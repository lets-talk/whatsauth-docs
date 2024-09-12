---
layout: default
title: WhatsAuth in Shopify
parent: Web Installation
grand_parent: Guides
---

# Guide to Using WhatsAuth Form Validator in Shopify

## Introduction

This guide will help you integrate the WhatsAuth Form Validator into a Shopify store to validate phone numbers via WhatsApp. This integration ensures that users entering phone numbers in forms, such as contact or checkout forms, are validated through WhatsApp before submission.

## Steps to Integrate WhatsAuth Form Validator in Shopify

### 1. **Add or Use an Existing Form in Shopify**

Shopify natively supports forms such as the **Contact Form** and custom forms that you may add to pages or product templates. To integrate WhatsAuth, the phone number input field in these forms will need to be validated.

You can either:
- Use Shopify’s default contact form
- Create a custom form using **HTML** and **Liquid** in Shopify templates

### 2. **Assign an ID to the Phone Number Input Field**

To validate the phone number, the input field must have a specific ID. You can add this directly to your form's HTML or Liquid template.

#### For the Contact Form:
1. Go to **Online Store > Themes > Actions > Edit Code**.
2. In the **Templates** section, find the `contact.liquid` file (or wherever your contact form is located).
3. Find the phone input field and assign it an ID like this:

```html
<input type="tel" id="phone_field" name="phone" placeholder="Phone Number" required>
```

#### For Custom Forms:
You can create a custom form in any Shopify page template:
1. In **Edit Code**, create a custom section or page where you want the form.
2. Add the following phone input field to your form:

```html
<form method="post" action="/contact">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" required>

  <label for="email">Email:</label>
  <input type="email" id="email" name="email" required>

  <label for="phone">Phone Number:</label>
  <input type="tel" id="phone_field" name="phone" required>

  <button type="submit">Submit</button>
</form>
```

Ensure the phone input field has the **ID** set to `phone_field` so it can be targeted by WhatsAuth.

### 3. **Add WhatsAuth Script to the Theme’s `<head>` Section**

1. In the **Edit Code** section of your Shopify theme, open the `theme.liquid` file.
2. Before the closing `</head>` tag, add the following code to load the WhatsAuth script:

```html
<script src="https://static.whatsauth.com/plugins/whatsauth-form/latest/validator.js"></script>
```

This will include the WhatsAuth Validator on every page of your Shopify store.

### 4. **Add Initialization Script to the Footer**

1. In the same `theme.liquid` file, scroll down to find the closing `</body>` tag.
2. Just before the `</body>` tag, add the following initialization script to target the phone input field:

```html
<script>
  window.$WhatsAuthForm.init({
    inputSelector: "#phone_field",  // The phone input field to validate
    apiKey: "YOUR_API_KEY",  // Replace with your actual WhatsAuth API key
    description: "Please verify your phone number using WhatsApp.",
    placeholder: "Click to validate your phone number",
    primaryColor: "#2ecc71",
    secondaryColor: "#27ae60",
    btnText: "Verify via WhatsApp"
  });
</script>
```

- Replace `"YOUR_API_KEY"` with your actual WhatsAuth API key.
- Ensure that `inputSelector: "#phone_field"` matches the ID of your phone input field.

3. **Save the changes** to your theme.

### 5. **Publish the Theme**

Once you have added the WhatsAuth script and initialization code, **save** and **publish your theme**. The phone number field on your form will now require WhatsApp validation before form submission.

### 6. **Customizing the Checkout Page (Optional)**

If you want to add WhatsAuth validation to phone number fields during checkout, you will need to modify the **checkout.liquid** template (available in Shopify Plus only). Follow a similar process to add the phone input ID and the WhatsAuth initialization script.

### 7. **Optional: Customizing Form and Styles**

You can further customize the phone input field or form styles by adding custom CSS to your Shopify theme.

1. In **Edit Code**, open your `theme.css` or `theme.scss` file.
2. Add CSS to style the phone number input field:

```css
#phone_field {
  border: 2px solid #2ecc71;
  padding: 10px;
  font-size: 16px;
  width: 100%;
}
```

This will apply custom styling to the phone input field on your form.

### Additional Notes

- **Customization Flexibility**: You can use the `inputSelector` to target other fields by modifying the selector (ID, class, or attribute). Be sure that the ID or selector you choose matches the phone input field in your form.
- **Checkout Page Limitations**: For modifying checkout fields, you'll need Shopify Plus, as the `checkout.liquid` file is only accessible in that plan.

By following these steps, you’ll successfully integrate the WhatsAuth Form Validator into your Shopify store, ensuring secure phone number validation via WhatsApp.


## Reference

For more detailed information on adding custom code to your Shopify theme, please refer to the official Shopify documentation:

[Shopify: Edit Theme Code](https://help.shopify.com/en/manual/online-store/themes/theme-structure/sections-and-settings/add-html)

This guide provides comprehensive instructions on how to modify your Shopify theme code, which is essential for implementing the WhatsAuth Form Validator and customizing your store's functionality.

