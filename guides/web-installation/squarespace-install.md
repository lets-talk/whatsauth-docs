---
layout: default
title: WhatsAuth in Squarespace
parent: Web Installation
grand_parent: Guides
---

# Guide to Using WhatsAuth Form Validator in Squarespace

## Introduction

This guide will help you integrate the WhatsAuth Form Validator into a Squarespace website to validate phone numbers via WhatsApp. This method ensures that phone numbers entered in your forms are verified before submission.

## Steps to Integrate WhatsAuth Form Validator in Squarespace

### 1. **Add or Use an Existing Form in Squarespace**

Ensure you have a form set up in Squarespace. You can use the **Form Block** to create a custom form.

1. In the Squarespace editor, go to the page where you want to add the form.
2. Click **Edit** on the page and add a **Form Block**.
3. Add the fields you need (e.g., name, email, and phone number).


This will set the **ID** of the phone number input to `phone_field` when the page loads.

### 2. **Add WhatsAuth Script to the Squarespace Header**

1. Go to **Settings** in your Squarespace dashboard.
2. Click on **Advanced** and select **Code Injection**.
3. In the **Header** section, paste the following code to include the WhatsAuth script:

```html
<script src="https://static.whatsauth.com/plugins/whatsauth-form/latest/validator.js"></script>
```

This ensures that the WhatsAuth Form Validator script is loaded on your site.

### 3. **Add Initialization Script to the Footer**

1. In the **Code Injection** settings, scroll to the **Footer** section.
2. Paste the following code to initialize the WhatsAuth Form Validator:

```html
<script>
  window.$WhatsAuthForm.init({
    inputSelector: "input[type='tel']",  // The phone input field to validate
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
- Ensure that `inputSelector: "input[type='tel']"` matches the desired phone input field.

{.highlight}
Since Squarespace doesn't allow setting ID on form fields, we use the type tel as a selector.

### 4. **Publish Your Squarespace Site**

Once you've added the code to the **Header** and **Footer** sections, save the changes and **publish your site**. The phone number input field will now require WhatsApp validation before the form can be submitted.

### 6. **Optional: Customize Your Form and Styles**

You can customize the appearance of the phone input field and form elements directly within Squarespace's style settings, or by adding custom CSS.

This will apply custom styles to the phone input field.

## Important Notes

- **Custom Form Fields**: Squarespace does not allow setting an ID on form fields directly in the form builder. However, using JavaScript to assign the ID (as shown in Step 2) allows you to target the phone field for WhatsAuth integration.
  
- **Code Injection**: Make sure that the script added in the Header and Footer is correct and that your form input field is properly targeted.

By following these steps, you will successfully integrate the WhatsAuth Form Validator into your Squarespace form, allowing for secure phone number validation via WhatsApp.


## Reference

For more detailed information on adding custom code to your Squarespace site, please refer to the official Squarespace documentation:

[Squarespace: Injecting Custom Code](https://support.squarespace.com/hc/en-us/articles/206543167-Adding-custom-code-to-your-site)

This guide provides comprehensive instructions on how to use the Code Injection feature in Squarespace to add custom HTML, CSS, and JavaScript to your site, which is essential for implementing the WhatsAuth Form Validator.

