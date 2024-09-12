---
layout: default
title: WhatsAuth in Webflow
parent: Web Installation
grand_parent: Guides
---

# Guide to Using WhatsAuth Form Validator in Webflow

## Introduction

This guide will help you integrate the WhatsAuth Form Validator into your Webflow project to validate phone numbers via WhatsApp. You will learn how to configure the phone number input field and set up custom code to enhance your form's functionality.

## Steps to Integrate WhatsAuth Form Validator in Webflow

### 1. **Prepare Your Webflow Form**

Ensure you have a form in Webflow, particularly with a phone number input field where validation will occur.

### 2. **Set an ID for the Phone Number Input Field**

1. Go to **Webflow Designer**.
2. Select your form block, then click on the phone number input field.
3. In the right-hand **Element Settings** panel, scroll to the **ID** section.
4. Set the **ID** to `phone_field`.

   Example:
   - **ID:** `phone_field`
   
   This ID is essential for targeting the phone field in your custom JavaScript code.

### 3. **Add Custom Code to the Webflow `<head>` Section**

1. Navigate to the **Project Settings** of your Webflow site.
2. Click on the **Custom Code** tab.
3. In the **Head Code** section, add the following script to load the WhatsAuth library:

```html
<script src="https://static.whatsauth.com/plugins/whatsauth-form/latest/validator.js"></script>
```

This script ensures that the WhatsAuth Form Validator is loaded on all your pages when published.

### 4. **Add Initialization Script to the `<body>` Section**

1. In **Project Settings**, go to the **Before Body Tag** section (also in **Custom Code**).
2. Paste the following initialization script:

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
- Ensure that the `inputSelector` matches the ID of your phone number field.

### 5. **Publish Your Webflow Site**

After adding the code to the `<head>` and `<body>` sections, **publish your Webflow site**. Your form's phone number input will now require WhatsApp-based validation before submission.

## Additional Notes

- **Customizing Styles**: You can use Webflow Designer to style the phone number input field. Custom styling for the WhatsAuth popup and button can be controlled via the configuration options in the initialization script.
  
- **Selector Flexibility**: You can target different phone number fields using various selectors (ID, class, etc.), but be sure the selector used in the custom code matches the field ID set in Webflow.

By following these steps, you’ll successfully integrate WhatsAuth Form Validator into your Webflow form, enhancing your site's security with WhatsApp phone number validation.


## References

For more information on adding custom code to your Webflow project, you can refer to the official Webflow documentation:

[Webflow University: How to add custom code](https://university.webflow.com/lesson/custom-code-in-the-head-and-body-tags)

This resource provides detailed instructions on how to add custom code to both the `<head>` and `<body>` sections of your Webflow site, which is crucial for implementing the WhatsAuth Form Validator.



