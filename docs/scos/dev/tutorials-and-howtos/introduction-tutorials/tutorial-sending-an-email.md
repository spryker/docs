---
title: "Tutorial: Sending an email"
description: The tutorial provides code samples on how to process customer registration information in Zed to register the customer and send a confirmation email.
last_updated: Sep 27, 2021
template: howto-guide-template
originalLink: https://documentation.spryker.com/2021080/docs/sending-an-email
originalArticleId: cdce91fc-fc1b-40f5-9442-b88f5036c86c
redirect_from:
  - /2021080/docs/sending-an-email
  - /2021080/docs/en/sending-an-email
  - /docs/sending-an-email
  - /docs/en/sending-an-email
  - /v6/docs/sending-an-email
  - /v6/docs/en/sending-an-email
---

The following example represents a real-world scenario: `CustomerRegistration`.

A customer goes through the registration process in your frontend (Yves) and all customer information is sent to Zed. Zed uses the information to register the customer. Once the registration is completed, the customer receives a confirmation email.

## 1. Handle mail usage

In the model which handles the registration, you can override the `sendRegistrationToken` function:

```php
<?php

namespace Pyz\Zed\Customer\Business\Customer;

use Generated\Shared\Transfer\CustomerTransfer;
use Generated\Shared\Transfer\MailTransfer;
use Spryker\Zed\Customer\Business\Customer\Customer as SprykerCustomer;
use Spryker\Zed\Customer\Communication\Plugin\Mail\CustomerRegistrationMailTypePlugin;

class Customer extends SprykerCustomer
{
    /**
     * @param \Generated\Shared\Transfer\CustomerTransfer $customerTransfer
     *
     * @return bool
     */
    protected function sendRegistrationToken(CustomerTransfer $customerTransfer)
    {
        // Create a MailTransfer instance which is
        // used for further processing
        $mailTransfer = new MailTransfer();

        // Set the mail type which is used for the
        // internal mapping—for example, which mail provider
        // should send this mail
        $mailTransfer->setType(CustomerRegistrationMailTypePlugin::MAIL_TYPE);

        // Set the CustomerTransfer to the MailTransfer
        // this can be any Transfer object which is
        // needed in the Mail
        $mailTransfer->setCustomer($customerTransfer);

        // Set the LocaleTransfer which should be used
        // for, for example, translation inside your templates
        $mailTransfer->setLocale($customerTransfer->getLocale());

        // Trigger the mail facade to handle the mail
        $this->mailFacade->handleMail($mailTransfer);
    }
}
```

Also, override factory:

```php
<?php

namespace Pyz\Zed\Customer\Business;

use Pyz\Zed\Customer\Business\Customer\Customer;
use Spryker\Zed\Customer\Business\Customer\CustomerInterface;
use Spryker\Zed\Customer\Business\CustomerBusinessFactory as SprykerCustomerBusinessFactory;

class CustomerBusinessFactory extends SprykerCustomerBusinessFactory
{
    /**
     * @return \Spryker\Zed\Customer\Business\Customer\CustomerInterface
     */
    public function createCustomer(): CustomerInterface
    {
        $config = $this->getConfig();

        $customer = new Customer(
            $this->getQueryContainer(),
            $this->createCustomerReferenceGenerator(),
            $config,
            $this->createEmailValidator(),
            $this->getMailFacade(),
            $this->getLocaleQueryContainer(),
            $this->getStore(),
            $this->createCustomerExpander(),
            $this->getPostCustomerRegistrationPlugins()
        );

        return $customer;
    }
}
```

All `MailTransfers` need to know which mail type (nothing more than a string) must be used for further internal processing.

A simple example is as follows:

```php
protected function sendRegistrationToken()
{
    $mailTransfer = new MailTransfer();
    $mailTransfer->setType(YourMailTypePlugin::MAIL_TYPE);
    $this->mailFacade->handleMail($mailTransfer);
}
```

## 2. Creating a MailTypePlugin

Create the `MailType` plugin for this example. For more information about creating a `MailTypePlugin`, see [HowTo: Create and register a MailTypePlugin](/docs/scos/dev/tutorials-and-howtos/howtos/howto-create-and-register-a-mailtypeplugin.html):

<details><summary markdown='span'>Code sample:</summary>

```php
<?php

namespace Pyz\Zed\Customer\Communication\Plugin\Mail;

use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface;
use Spryker\Zed\Mail\Dependency\Plugin\MailTypePluginInterface;

class CustomCustomerRegistrationMailTypePlugin extends AbstractPlugin implements MailTypePluginInterface
{
    public const MAIL_TYPE = 'custom customer registration mail';

    /**
     * @api
     *
     * @return string
     */
    public function getName(): string
    {
        return static::MAIL_TYPE;
    }

    /**
     * @api
     *
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return void
     */
    public function build(MailBuilderInterface $mailBuilder): void
    {
        $this
            ->setSubject($mailBuilder)
            ->setHtmlTemplate($mailBuilder)
            ->setTextTemplate($mailBuilder)
            ->setSender($mailBuilder)
            ->setRecipient($mailBuilder);
    }

    /**
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return $this
     */
    protected function setSubject(MailBuilderInterface $mailBuilder)
    {
        $mailBuilder->setSubject('mail.customer.registration.subject');

        return $this;
    }

    /**
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return $this
     */
    protected function setHtmlTemplate(MailBuilderInterface $mailBuilder)
    {
        $mailBuilder->setHtmlTemplate('customer/mail/customer_registration.html.twig');

        return $this;
    }

    /**
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return $this
     */
    protected function setTextTemplate(MailBuilderInterface $mailBuilder)
    {
        $mailBuilder->setTextTemplate('customer/mail/customer_registration.text.twig');

        return $this;
    }

    /**
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return $this
     */
    protected function setRecipient(MailBuilderInterface $mailBuilder)
    {
        $customerTransfer = $mailBuilder->getMailTransfer()->requireCustomer()->getCustomer();

        $mailBuilder->addRecipient(
            $customerTransfer->getEmail(),
            $customerTransfer->getFirstName() . ' ' . $customerTransfer->getLastName()
        );

        return $this;
    }

    /**
     * @param \Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface $mailBuilder
     *
     * @return $this
     */
    protected function setSender(MailBuilderInterface $mailBuilder)
    {
        $mailBuilder->setSender('mail.sender.email', 'Custom email sender name');

        return $this;
    }
}
```

</details>

The `Mail` module’s default `MailBuilder` is already pre-defined to build the `MailTransfer`. `MailBuilder` internally adds a new `MailRecipientTransfer` with the passed information, email, and name.

## 3. Registering a plugin

When the plugin is created, it must be registered in `MailDependencyProvider`:

```php
<?php
        ...
        $container->extend(self::MAIL_TYPE_COLLECTION, function (MailTypeCollectionAddInterface $mailCollection) {
            ....
            $mailCollection->add(new CustomCustomerRegistrationMailTypePlugin());

            return $mailCollection
        });
        ...
 ?>
```

## 4. Mail translations

The default `MailBuilder` also has access to the glossary with the `setSubject()` method. This is used for translations as follows:

```php
<?php
namespace Pyz\Zed\Customer\Communication\Plugin\Mail;

use Spryker\Zed\Kernel\Communication\AbstractPlugin;
use Spryker\Zed\Mail\Business\Model\Mail\Builder\MailBuilderInterface;
use Spryker\Zed\Mail\Dependency\Plugin\MailTypeInterface;

class CustomerCustomerRegistrationMailTypePlugin extends AbstractPlugin implements MailTypePluginInterface
{
    ...
    protected function setSubject(MailBuilderInterface $mailBuilder)
    {
        $mailBuilder->setSubject('mail.customer.registration.subject');
    }
    ...
}
```

A string is used as a key of the translation. The `MailBuilder` internally does the translation through `GlossaryFacade`:

```php
<?php
namespace Spryker\Zed\Mail\Business\Model\Mail\Builder;

    ...

    protected function setSubject($subject, array $data = [])
    {
        $subject = $this->translate($subject, $data);

        $this->getMailTransfer()->setSubject($subject);

        return $this;
    }
    ...

    protected function translate($keyName, array $data = [])
    {
        $localeTransfer = $this->getLocaleTransfer();

        if ($this->glossaryFacade->hasTranslation($keyName, $localeTransfer)) {
            $keyName = $this->glossaryFacade->translate($keyName, $data, $localeTransfer);
        }

        return $keyName;
    }
}
```

As you can see above, you can also translate with the placeholder. For the `mail.order.shipped.subject` key, you have `Your order {orderReference} is on its way as translation`.

In your `MailType` plugin, you can use the `orderReference` from the given `OrderTransfer` within the subject:

```php
<?php
...
protected function setSubject(MailBuilderInterface $mailBuilder)
{
    $orderTransfer = $mailBuilder->getMailTransfer()->getOrder();

    $mailBuilder->setSubject(
        'mail.order.shipped.subject',
        [
            '{orderReference}' => $orderTransfer->getOrderReference()
        ]
    );
}
...
}
...
}
```

## Set templates

Usually, you have a `.twig` file which contains the template you want to use for mail. 

Set the template which must be used in your `MailType` plugin:

```php
<?php
...
protected function setTextTemplate(MailBuilderInterface $mailBuilder)
{
    $mailBuilder->setTextTemplate('customer/mail/customer_registration.text.twig');
}
...
}
```

The provider determines the template's final look. It can contain plain text or HTML. For example, you can even have a template that generates JSON:

```twig
{
    ...
    customer: "{% raw %}{{{% endraw %} mail.customer.firstName {% raw %}}}{% endraw %} {% raw %}{{{% endraw %} mail.customer.lastName {% raw %}}}{% endraw %}",
    ...
}
```

In the following example, you have a plain text template with:

```twig
{% raw %}{{{% endraw %} 'mail.customer.registration.text' | trans {% raw %}}}{% endraw %}
```

The templates must be placed within the module's `Presentation` layer—fpr example, `src/Pyz/Zed/Customer/Presentation/Mail/customer_registration.text.twig`. You can use the same trans filter as used with Yves and Zed templates.

`TwigRenderer` is the default renderer, but you can add your own renderer by implementing `RendererInterface`.

We also provide a basic layout file, where you can inject concrete content files into. If you want to build your own layout, you need the following in your template:

```twig
{% raw %}{%{% endraw %} for template in mail.templates {% raw %}%}{% endraw %}
    {% raw %}{%{% endraw %} if not template.isHtml {% raw %}%}{% endraw %}
        {% raw %}{%{% endraw %} include "@" ~ template.name with {mail: mail} {% raw %}%}{% endraw %}
    {% raw %}{%{% endraw %} endif {% raw %}%}{% endraw %}
{% raw %}{%{% endraw %} endfor {% raw %}%}{% endraw %}
```

The preceeding template is used for plain text messages, and templates can also be used to generate JSON or query strings like `customer={% raw %}{{{% endraw %} mail.customer.firstName {% raw %}}}{% endraw %}&orderReference={% raw %}{{{% endraw %} mail.order.orderReference {% raw %}}}{% endraw %}`. It’s up to your provider to decide what to render.

For HTML messages, you need to have this in your layout file:

```twig
{% raw %}{%{% endraw %} for template in mail.templates {% raw %}%}{% endraw %}
    {% raw %}{%{% endraw %} if template.isHtml {% raw %}%}{% endraw %}
        {% raw %}{%{% endraw %} include "@" ~ template.name with {mail: mail} {% raw %}%}{% endraw %}
    {% raw %}{%{% endraw %} endif {% raw %}%}{% endraw %}
{% raw %}{%{% endraw %} endfor {% raw %}%}{% endraw %}
```

When you complete the steps, to activate the mail functionality, call `MailFacade::handleMail()`.
