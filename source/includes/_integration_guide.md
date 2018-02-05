# Divido Integration Guide

An overview of how to integrate Divido as a payment option in a webshop.

This document assumes you're developing a reusable plugin to a shop system. If you are adding Divido to a custom built webshop or as a one off integration, some of the sections, such as the settings, might not apply to your case.

Date: 19 Jan 2018 Version: 0.9

## The Divido Process

An overview of the steps a customer goes through when checking out using Divido as the payment method:

|#  |Where |Webhook|What's Happening |
|---|----------|---|-----------------|
|1  | Merchant |N   |Choose Divido as payment method, Select financing plan and deposit percentage|
|2  |Merchant  |N  |Confirm, redirections to ...|
|3  |Divido    |Y  |Start of Divido application process|
|4  |Divido    |Y  |Enter personal and banking info|
|5  |Divido    |Y  |Pay deposit|
|6  |Divido    |Y  |Sign Contract|
|7  |Divido    |N  |Thank you page, redirection to ...|
|8  |Merchant  |N  |Success Page|

## Sequence Guide

![sequence diagram](/images/sequence-diagram.png)

# Parts of the integration 

## Global settings
To provide the merchant with the possibilites to customise their Divido integration so that it suits their business, you need to add a list of options to the payments section of the webshop settings.

Below is a list of what should minimally be included in this list. More options are discussed under the section `Limiting available payment plans`.

Please note that the names of the options are only guidelines and can be changed to suit the shops' platform.

### API Key
Type: String
Example: `sandbox_ccdc53735.b04d5a8270cf7cf8d24238e5a2a5fe4f` Contains the API key necessary for communication with Dividos services.

### Enabled
Type: Bool
For quickly enabling/disabling the Divido payment option and product page calculator

### Title
Type: String
Lets the customer pick their own title for the payment option at checkout

### Show product page widget
Type: Bool
Toggles the product page widget

### Order status on creation
Type: Order status
Provide a list of possible/applicable order statuses, so that the merchant can choose what status an order created by Divido gets.

### Order creation level
Type: String
Possible values: `ACCEPTED`, `SIGNED`
Lets the merchant choose when in the Divido process an order is created/escalated.

### Send automatic fulfilment update
Type: Bool
Toggles whether or not the plugin sends an automatic update call to Divido, when a Divido order reaches a certain status.

### Fulfilment status
Type: Order status
If "Send automatic fulfilment update" is True, this is the order status it would react to.

### Cart amount limit
Type: Float
Lets the merchant define an amount, under which a cart is not eligible to be paid for with Divido.

### Product selection
Options: All products, Products above specified price
Above is the two required options, see more under "Limiting available payment plans"

### Product price limit
Type: Float
If "Product selection" is set to "Products above specified price", this is the price limit against which products are checked.

## Merchant specific javascript
For every customer, Divido provides a javascript generated specifically for them. This javascript contains functionality for showing dynamic calculators and widgets, as well as info about available financing products. Since this script is regenerated when the customers plans are updated, it should not be hosted locally, but sourced from Dividos CDN.

The URL of the script follows this pattern: `//cdn.divido.com/calculator/[API KEY].js` The `[API KEY]` placeholder is replaced by the part of the API key up to the period.

So if the API key is `sandbox_ccdc53735.b04d5a8270cf7cf8d24238e5a2a5fe4f`
The part we use for the javascript URL is `sandbox_ccdc53735`

Example: `//cdn.divido.com/calculator/sandbox_ccdc53735.js`

This script needs to be included on the product page and the checkout page and anywhere else you want to display a Divido calculator or widget.

## Product page widget

The Divido product page widget allows the customer to get a quick overview of what financing options are available on that specific product and what different levels of deposit will do for the overall cost.

In its most basic form, it looks like this:
> In its most basic form, it looks like this HTML:

```html
 <div data-divido-widget data-divido-amount="[PRODUCT PRICE]"></div>
 ```

**Example: TODO -INSERT EXAMPLE HERE!!!**

We suggest you place it directly under the price on the product page. Don't forget to take the values of the "Product selection" and "Product price limit" into account when deciding whether or not to show it!

It's only the tag that's needed, the Divido javascript will take care of the rest.

## Checkout form

When the customer has chosen Divido as their payment option, you need to provide them with a form where they can choose financing, product and set a deposit amount. 

> This is what the markup looks like in our Magento plugin HTML:

```html
<fieldset data-divido-calculator data-divido-amount="[GRAND TOTAL]">
     <h1>Pay in instalments</h1>
     <dl>
         <dt><span data-divido-choose-finance data-divido-label="Choose your plan"
 data-divido-form="divido_finance"></span></dt>
         <dd><span class="divido-deposit" data-divido-choose-deposit data-divido-la
 bel="Choose your deposit" data-divido-form="divido_deposit"></span></dd>
     </dl>
     <div class="description">
         <strong>
             <span data-divido-agreement-duration></span> monthly payments of <span
  data-divido-monthly-instalment></span>
         </strong>
     </div>
     <div class="divido-info">
         <dl>
             <dt>Term</dt>
             <dd><span data-divido-agreement-duration></span> months</dd>
             <dt>Monthly instalment</dt>
             <dd><span data-divido-monthly-instalment></span></dd>
             <dt>Deposit</dt>
             <dd><span data-divido-deposit></span></dd>
             <dt>Cost of credit</dt>
             <dd><span data-divido-finance-cost-rounded></span></dd>
             <dt>Total payable</dt>
             <dd><span data-divido-total-payable-rounded></span></dd>
             <dt>Total interest APR</dt>
             <dd><span data-divido-interest-rate></span></dd>
          </dl> 
      </div>
     <div class="clear"></div>
     <p>You will be redirected to Divido to complete this finance application when
 you place your order</p>
 </fieldset>
```

Again, the Divido javascript will take care of making this form interactive. When the customer has chosen financing plan and deposit, you need to collect that data and send it, along with additional information about the order and the customer, to make a credit request.

## Credit request

The first step in a credit application starts with a credit request. It's simply a HTTP POST call to our web service, containing customer and order data that's used as the basis for the credit application.

You can see the full documentation for this call in the credit request section of our API documentation. Please note that the host name differs depending on whether you're using a live or sandbox key, see API
endpoints.

If the call is correctly done, the response will contain a field named "url". To start the credit application, redirect the user to that URL.

The customer has now left the merchants shop and is walked through a series of steps in the Divido credit application process. Each of those steps results in an update call back to your server, Webhooks.

## Handling Webhooks (automatic updates from Divido)

Whenever the customer completes a step in the credit application process, an HTTP POST call is sent to the URL specified in the credit request field "response_url".

These are the events we send updates for, and a list of their possible statuses:

+ Basic application is finished 
    + ACCEPTED
    + REFERRED 
    + DECLINED

+ Basic application has been cancelled by customer 
    + CANCELLED
+ Deposit has been paid 
    + DEPOSIT-PAID
+ Contracts have been signed 
    + SIGNED
+ Merchant marks order as fulfilled 
    + ACTION-LENDER

When the application is done, the information is sent to the underwriter for review. This is a mostly automated process and the application gets accepted or declined directly. 

In some cases, however, the underwriter will have to do a manual review of the application and its status is set to "referred". This will pause the application process and the customer will be given the choice to wait for the approval process to finish or return to the merchant. 

When referred, the approval process takes up to 3 days and when it's done, the customer gets an email with a link that places them right where they left off in the application process.
> Here's an example of the payload:

```json         
   {
     "application": 'C84047A6D-89B2-FECF-D2B4-168444F5178C',
     "reference": 100024,
     "status": 'SIGNED',
     "live": true,
     "metadata":  {
        "Invoice Number":"844001",
        "Order Number":"100019"
     }
}
```

Field for field, this is the contents:

**application**: The ID of the Application, we recommend you save this for further reference.

**reference**: Third part reference, if sent with credit request
status: This is the actual status update!

**live**: Whether or not this comes from our live environment (false = sandbox environment)

**metadata**: This contains whatever you sent us in in the metadata field when you did the credit request.

## Security
To make sure no one is falsely sending you status updates, you need to verify that the updates are actually from us and that they refer to a actual orders. To acheive this, we usually create a unique salt, store it together with the order id, create a hash based on the salted order id and send the hash and the order id in the credit request metadata. When the status updates comes back, we salt the order id, hashes it and checks it agains the hash that's in the metadata.

## Limiting available payment plans
Merchants often need to tailor the list of available financing plans to suit their current situation. To allow this you need to provide a way to limit the overall available financing plans and often more granualar settings targeting categories, brands or individual products.

What's needed really comes down to the individual merchant. Here we will detail the solution we ship with our generic Magento plugin.

### Global settings

**Shown plans** Options: All plans, Selected plans

### Available plans
Type: List of strings

Dependencies: Only shown if **Shown plans** is set to "Selected plans" Multiple select box/List of checkboxes with the result from a call to our API (http://developer.divido.com/#resources-finances).

### Product selection
Extra option: Selected products
When this is option is chosen, a product is only available on finance if it has specifically been enabled. Used in combination with Shown plans set to "Selected plans".

### Product settings 

### Available on finance
Options: Default settings, Selected plans

### Available plans
Type: List of strings
Dependencies: Only shown if Available on finance is set to "Selected plans" Multiple select box/List of checkboxes with the result from a call to our API (http://developer.divido.com/#resources-finances).

### Calculating available financing plans

You need to calculate the available financing plans on both the product page. How you do it on the checkout page depends on your use case, but we will show how we do it in our generic plugins as an example.

### Product

> Naive pseudo code:

```
 If global setting "Product selection" is "Selected products"
     If product setting "Available plans" is "Default settings"
         Let Plans be global setting "Available plans"
     Else
         Let Plans be product setting "Available plans"
     Let Plans be global setting "Available plans"
 Return Plans that has a minimum price lower than the product price
```

### Cart
> Naive pseudo code:

```
 For each product in the cart
     Collect all plans for the product
 Return all plans that has a minimum price lower than the full order value
 Else
 ```