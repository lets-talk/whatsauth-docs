---
layout: default
title: WhatsAuth in Wix
parent: Web Installation
grand_parent: Guides
---

# Guide to Using WhatsAuth Form Validator in Wix

## Introduction

This guide will help you integrate the WhatsAuth Form Validator into a Wix website to validate phone numbers via WhatsApp. This validation ensures that the phone numbers entered are verified before submission.

## Steps to Integrate WhatsAuth Form Validator in Wix

### 1. **Create or Use an Existing Form in Wix**

First, ensure you have a form in Wix where you want to validate phone numbers. You can use Wix Forms, Wix's native form builder, or custom HTML forms added through the **HTML Embed** option.

If you are using Wix Forms:
1. Go to your site’s editor.
2. Add a phone input field to your form.

If you are embedding a custom HTML form using the **Embed Code** element, make sure it contains a phone input field with an ID, like this:

```html
<form id="contactForm">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>

    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>

    <label for="phone">Phone Number:</label>
    <input type="tel" id="phone_field" name="phone" required>

    <button type="submit">Submit</button>
</form>
```

### 2. **Add WhatsAuth Script to the Wix Header**

1. Go to your **Wix Dashboard**.
2. In the left-hand menu, click on **Settings**.
3. Scroll down and select **Custom Code**.
4. Click on **+ Add Custom Code**.
5. Paste the following script into the **Head** section:

```html
<script src="https://static.whatsauth.com/plugins/whatsauth-form/latest/validator.js"></script>
```

6. Set this script to **Load on all pages**.

This ensures that the WhatsAuth Form Validator script is loaded on all the pages of your Wix website.

### 3. **Add Initialization Script to the Footer**

1. In the **Custom Code** settings, click on **+ Add Custom Code** again.
2. Select the **Body - End** section for the placement.
3. Paste the following script:

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
- Ensure the `inputSelector` matches the ID of your phone input field (e.g., `#phone_field`).

4. Set this script to **Load on specific pages** if you only want it to run on form pages, or **Load on all pages** if applicable.

### 4. **Publish Your Wix Site**

Once the custom code is set up, **publish your Wix site**. The phone number input field will now require WhatsApp-based validation before the form can be submitted.

### 5. **Adding Custom HTML Forms (Optional)**

If you’re not using Wix’s form builder and want to create your own custom form, you can embed it using the **HTML Embed** element:
1. In the **Wix Editor**, go to the page where you want to add the form.
2. Click **Add** > **Embed** > **Embed HTML**.
3. Paste your custom HTML form code, ensuring the phone input field has the correct ID (`#phone_field` or another custom selector).

Example of custom HTML form:

```html
<form id="contactForm">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>

    <label for="phone">Phone Number:</label>
    <input type="tel" id="phone_field" name="phone" required>

    <button type="submit">Submit</button>
</form>
```

### 6. **Customizing Styles**

You can adjust the styles of your form elements using the Wix Editor for built-in forms or by embedding CSS in custom HTML forms.

For custom HTML forms, you can add your own CSS inside the **Embed Code** element:

```html
<style>
  input[type="tel"] {
    border: 2px solid #2ecc71;
    padding: 10px;
    font-size: 16px;
  }
</style>
```

## Important Notes

- **Form Builder Integration**: If you use the Wix Forms builder, ensure the phone number field is properly targeted using the correct ID or CSS selector. The WhatsAuth script will only work with phone input fields that have the correct ID set.
  
- **Styling**: Customize your form's appearance directly within the Wix Editor or through custom CSS in embedded forms.

By following these steps, you'll successfully integrate WhatsAuth Form Validator into your Wix form to validate phone numbers via WhatsApp.


## References

For more information on adding custom code to your Wix site, you can refer to the official Wix documentation:

[Wix Help Center: Adding Custom Code to Your Site](https://support.wix.com/en/article/embedding-custom-code-on-your-site)

This resource provides detailed instructions on how to add custom HTML, CSS, and JavaScript to your Wix site, which is crucial for implementing the WhatsAuth Form Validator and customizing your site's functionality.

