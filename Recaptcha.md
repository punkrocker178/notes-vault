# V2
- I am not a robot check box , if suspicious will challenge user
## Pros
- Simple implementation
- Block majority of simple bots without further actions
## Cons
- High risk of being solved by bots
- Can be hard for human + add frustration => Low conversion rate
- Lacking accessibility (visually impaired, colorblind)

# V2 Invisible
- Does not show checkbox, can be manually triggered on button clicked. If suspicous will challenge user

# V3
- Evaluates user to be human or bot through an assessment. Returns score for further analysis. No user interaction required.
- We have to manually mark each section of the website that needs human verification
## Pros
- No user interaction
## Cons
- Needs large volume of data for scoring evaluation
- Have to make decision to indicate whether human or bot (what to do for each score)

# Thoughs on V3
- Since there are no user interaction with recaptcha, so we can only restrict the UI if user is a bot. In false positives cases, this can be very annoying for the user.
- Using both version and V3 fallback to V2 usecase are mentioned in several places but there are no article about it.

**Suggestion**: Use both V3 and V2 
- If the score is low, we can show the v2 checkbox to the user
- Or: Hide submit/ actions button in a form

**Scenario**
1. Bot user submit form with v3 site key token to v3 key endpoint (Low score) 
2. Frontend show captcha challenge 
3. User solve challenge 
4. Sovled token is from v2 site key
5. Submit form with v2 key endpoint

**Current problem**
When combine both V3 and V2 we need 2 site keys.  Each site key needs a corresponding backend to handle assessments.
The scenario provide a solution to false-positives cases. But not by a large margin, as some bots can solve captchas or human give wrong answer on hard captchas.

# Other thoughts
- Other competitors trying to make captcha solutions less reliable than their products by talking about captchas can be easily solved, degrade user experiences,  etc... 
- [NopeCha](https://developers.nopecha.com/) is a captcha solver provides API and browser extensions

# Final thoughts
- Nothing is perfect, we have to use what we have, some protection is better than no protection. 
- After reviewing the [reCaptcha key type](https://cloud.google.com/recaptcha-enterprise/docs/choose-key-type?_ga=2.168949601.-1513688254.1702368217#differences-keys)  and [reCaptcha caveats](https://cloud.google.com/recaptcha-enterprise/docs/choose-key-type?_ga=2.168949601.-1513688254.1702368217#captcha-challenges), the opphub register page can be v2 or v3 (currently v3). The login page can use v2 just for some extra protection, then we can layer v3 in other parts of the opphub (add clarifications, download documents, submit response/bid, etc...)

# Useful links
[Use V2 and V3](https://developers.google.com/recaptcha/docs/faq#can-i-run-recaptcha-v2-and-v3-on-the-same-page)
[Create reCAPTCHA Enterprise key]([Create reCAPTCHA keys for websites  |  reCAPTCHA Enterprise  |  Google Cloud](https://cloud.google.com/recaptcha-enterprise/docs/create-key-website#create-recaptcha-key-console))