# V2
- I am not a robot check box
- Simple implementation

# V3
- Evaluates user to be human or bot through an assessment. Returns score for further analysis. No user interaction required.
- We have to add config to each section of the website that needs human verification

# Thoughs on V3
Since there are no user interaction with recaptcha, so we can only restrict the UI if user is a bot. In false positives cases, this can be very annoying for the user.

**Suggestion**: Use both V3 and V2 
- If the score is low, we can show the v2 checkbox to the user
- Or: Hide submit/ actions button in a form

# Useful links
[Use V2 and V3](https://developers.google.com/recaptcha/docs/faq#can-i-run-recaptcha-v2-and-v3-on-the-same-page)
[Create reCAPTCHA Enterprise key]([Create reCAPTCHA keys for websites  |  reCAPTCHA Enterprise  |  Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/create-key-website#create-recaptcha-key-console))