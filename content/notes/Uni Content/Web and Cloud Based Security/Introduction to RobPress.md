# Introduction to RobPress

## PHP Files

- Anything not in PHP tags is output directly (HTML).
- Use `<?php... ?>` tags to execute PHP code.
- Use `<?= .. ?>` to output PHP code (echo).

![PHP Files](https://remnote-user-data.s3.amazonaws.com/ED4cuhpToQSKhYDbwiifOqGr_qQC8n3tNFclKn_xvciqm_6lHNpT3i6QyHkF3vWaOBef5t5BZxc8CfjSHL6NbCid4XNzZBEvlNZz8dIHEOEp5IB2b__HTLPpbyNBOqD-.png)

## Functions

- Define a function using function keyword.
- Optional parameters are assigned default values using =.
![Functions](https://remnote-user-data.s3.amazonaws.com/vBxnwPFjD2zNGM6BMn-7RzxFUPdGl6dSqY9oWAEvWiFghEKEgN_Pabql1W1_9hSoaZZ308l2_Czle-zveIn7MjL6qVV4VTNXuzN0tWOqN_zYFsgsC0HKAkEctG1wJJTb.png)

## Variables

![Variables](https://remnote-user-data.s3.amazonaws.com/j9apfpD5Y0hCh_2lwl8vKqKgsVJ1O5_H29TPNNnW81IO2MfqwJmlUt9qxSigy902QltrFpGolmYDhoHDRoDZwBKsNH5BQSY9rKzVX-W5XdQZJJDOWkBATScy02KwtgIs.png)

## Arrays

- Create an array.
- Arrays can be numeric.
- Or associative (like hashmaps).
- Arrays can be initialised.
  - Or for associative arrays.
- Other array syntax.

## Built-in Variables (Arrays)

- `$_GET` - URL parameters.
- `$_POST` - Posted form values.
- `$_SERVER` - Information about the request which was made.

## Seeing inside Variables

- `print_r($variable)` or `var_dump($variable)`.

![|200](https://remnote-user-data.s3.amazonaws.com/2wqlo-llBKjDUBUKcQUrPpCHarjt5Fs8AhhoiT1UZKubfCtQO_UstETMNKaWW8xKWWk-LY1Rx3Xp5hE3pcux2N4PzoJ1vj3su13F6EpTSq2m0Ffa2YEd-CIBSzjUWB_2.png)

## Conditions

![|400](https://remnote-user-data.s3.amazonaws.com/PrpxJvAA2qJO0qVB2obzVv-BvLQ2poJgguoLA3_y9afd1yG1Ytqb8Vav1DU48wr3y3OalSKNM_Xu9_Qr34IjK7wwK7iJIaDxpRHk2_fiiI5uL67yugBeydg0NseB6VfM.png)

- You can also use conditions in short tags.

![|300](https://remnote-user-data.s3.amazonaws.com/-GvvXBkhoeJvsB9qrI_00eqXDQ19Rc_iUI8HRHhBn-hl76wF5yguQj498j73lxN4V7gjcWRmfEpyJdeisOlgQYoVStqgzdb6JnCP7Bpt00g5jRbXpb03Lt9-1_w6e6J6.png)

## Loops

- `foreach`.

![|400](https://remnote-user-data.s3.amazonaws.com/5ZQDO8w96iQm0eKKJsPJBG2j-4zt_NyDKKzG-BY9c1uWS94OIa7lMEPdlemQqRWi0A2Dn4XElz3EOV0s2Hmb1hTsM6lujrlvBmcOBXh6f9t3W_KycABBoB-wARJ2RIx5.png)

- Iterating through both keys and values.

![|400](https://remnote-user-data.s3.amazonaws.com/d-TSrljdU4kAlJdYR5C-vuTFbTI4eeHQCFEJMzE6XhC2YVfz-AMlahDPZLuXt3De03Jp5OeTnn4KpSkIcEEIkX-3cnI9RYrXyaFzofNkJA9qB5SDczcR01ASEKGtvsTC.png)

- Special syntax for loops using short tags.

![|400](https://remnote-user-data.s3.amazonaws.com/KrXJEvm5B8HD4zcsCO_OYrw50i119bEVn0ZWmbnz-0yuicdHrvj8yAH3ZIBPZdgw41i-tsXNe8iktZrQFlpJ86KTuXTQsKa2NSHbFv1RqTvbxVylKrFWlH-_h_ScmapK.png)

## FatFree

- Maps URLs to PHP functions.

![FatFree](https://remnote-user-data.s3.amazonaws.com/FJOnFtD03dBnAc67ESoQA65bPKnPAEB_uPg2bf5gZTJ7PkCMrjHfusSBKJil1qOAqvAxtdgwJh21wj6YkUjweGLStG9s2I3lXk-94v-fe49ZW-qnMYvNNCI4-Tpj7JGv.png)

## Main Areas of RobPress

- Public:
  - Blog.
  - User.
  - Page.
- Private - Admin:
  - Comments.
  - Posts.
  - Settings.
  - Page.
  - Users.
  - Categories.

## Using FatFree to Automatically Provide an MVC Structure

![MVC Structure 1](https://remnote-user-data.s3.amazonaws.com/ZdBQuHPbTXtycxz5zcZCIYnNuFg-cP-8RKQ4CRLMxnbrUAapYPcD1cjSazH_qz3CHPg0VsSkII-ByTuEWdj7uTIc9Mx9cnMgRH2-atExahi7lVNQBETimXurQ77lTBcN.png)

![|300](https://remnote-user-data.s3.amazonaws.com/xX8z3SobsFN2aGRFmrlZ6YxD99zfhgsfHsPWW05IP4hhlCjWyY9Jl24-2Q-9KtN_tyMUVTBm8za-fdCtZuiN81RSuN1JwRxToFkWScG9hEfP9l5STdiz1yxm7zD6GkFq.png)
### Example

![|400](https://remnote-user-data.s3.amazonaws.com/qYb5WJea37pCLbIaalbtIxywF7w5Jq_n8Ww-q4O1Yd7J-5M5_-Qc6QPKDvVS7p7qnfITxhqqmaVUkQdZo7PjCCpPXM_4Qlu7oX976ZoVItG8RVcCpFN0ChFFfZsOC5sn.png)

![|400](https://remnote-user-data.s3.amazonaws.com/hxm36A4wd27xWyFrkvsgDUZN9SrHaE_547OHP67HL_cALjRfmAEivp0M-gQ_BRabuSxX9nkeysQUiqjUhlGCWU6TEf2Wu5TZrXzFHx8rpJ5zcCY2zDfygN7DimgR8Goh.png)

- `$f3` is the fatfree object.
- `PARAMS.3` accesses the third parameter (third bit of the URL).

## Using FatFree to Create Forms

![Form 1](https://remnote-user-data.s3.amazonaws.com/MD2zeat3WrbZXEzLhRce7j_FRZxVcZVBxIO644BiLqDIYuWytLreS13iWIXtL8tg9SAZKP2mE8_U0y7rKnlXMPlB3wRLz-S8CayeGLW9rivxpZ7OJErExLds46ULTFXW.png)

![Form 2](https://remnote-user-data.s3.amazonaws.com/o_cOvQB-pHbOmTbqt2SagoDJD_p4c-CjZj2Ooi7zfOvDGrW95XnxGkoZKcM8Fa2V-WQeIjkErSH_geKwF2A77l5X_Z3jSpTLuodcoshG-DlWdT11gxOf5fjw48UFA9UL.png)

![Form 3](https://remnote-user-data.s3.amazonaws.com/e6Ylg3KFsdtcfAKEMFoe_a6XAw2W_6_zXOVNl5Q2GHh0Ct9Btynq-c2HHWj-0hBd_qRD7Su6XsngZQgmoNaIu4NR9hUzuHCEwjmgZjxvwU_JNqKD4K31EOTdQvzAkli9.png)

## Templates can take Variables

- Maps `$variablename` inside the template to the `$variable` in the code.
![Template Variable 1](https://remnote-user-data.s3.amazonaws.com/MV92ThwaN95K-e4ETDRRPBY44glfoXm0rVU59sG5hD7qtCwGs26qfeCDqwF5W2gBHfZBhJchG6pEbLvZHvlgwRs9o0_FrFW4BrcHSHLP7yo3YXB74QbMMOsJ5ve3SQLk.png)
![Template Variable 2](https://remnote-user-data.s3.amazonaws.com/1kF_ldr9b2NI4Z6d1M01ENHOr0qvH8gBWLS8bFy2hpD9X52okefTinJAPozhbg-4F6NQfSQwpAR4LAp1SAaEiD_R65kXZxf3LDFjhokaki28sB43QksmqggJ8T1aHMh1.png)

## Models

- Model is a field on that controller.
  - It loads any of the models from that, which have functions.
- `$this` refers to the current controller.
### Model functions which all models have

- Will return a single result.
- Will return an array of results.
### Examples
![Model Example 1](https://remnote-user-data.s3.amazonaws.com/ZYiEmDh-VltHs98nbVizHVGQUdsYnpduV5YrjC28nENNMQqxJghJLp_4S1_xp-UOljH0ivXqW4A2T5FgZc6q12DRpR2K29KiypOOpoADXFj-HcFHwlWVwAiXeK7_Tex6.png)
### How are Results Returned?
- What is a DB mapped object.
  - But it also has functions attached to it for manipulation.
    - So you can also manipulate the database with it.
    - `$user - > id=5; $user⇒save();`
  - Like an array, can access using array/object notation.
    - `$user['id']` or `$user - > id`
- Multiple Results - An array of DB mapped objects.
- 1 Result - A single DB mapped object.
### Model Examples
#### Single Result - View a Blog Post
![Single Result](https://remnote-user-data.s3.amazonaws.com/pdvA77gUEUqq5XmhPIIBhbExHhhSk4ASGsZBWtEzM8p0Ou4Z9JSEzPepagbz9limlV5g0KHmIxVUoOjrPFHT1_14mDxixwEi9JstiVoffJIphJHmK-OENsppOxfBKmP7.png)
#### Multiple Result - Get all the Users
![Multiple Result](https://remnote-user-data.s3.amazonaws.com/TzZcW3-QB33meMgPNEjCviU6CKisLs74q4DGFhGbwcZENGijljtf2Z4UXQ_42Q_YCjz3ltt53EQ-KLLRia_750wvUJJ2GazT8006o7JYCB8aWMqTw4_f_u7Paw0aEtJc.png)

## The Security of the Web
### HTTP Requests
#### HTTP Verbs
- GET - Read
- POST - Create (or update/modify/delete/..)
- PUT - Update/Replace
- PATCH - Update/Modify
- DELETE

### Server Responses
#### 2xx - Success
- 200 - OK
#### 4xx - Client error
- 404 - Not found
- 400 - Bad request
- 403 - Forbidden
- 401 - Unauthorised
- 405 - Method not allowed
- 418 - I'm a teapot
#### 5xx - Server error
- 503 - Service unavailable
- 500 - Internal server error
#### 3xx - Redirect
- 304 - Not Modified (Cached)
- 302 - Found (Moved temporarily) (or 307)
- 301 - Moved permanently (or 308)
#### 1xx - Informational

### GETing by Hand
#### Methods
- 
- 
- 

### Passing in User Input
#### Using GET
- GET query parameters
  - 
#### Using POST
- POST form data
  - 

## Testing for Infrastructure as Code
### InfoSec Triangle
![InfoSec Triangle](https://remnote-user-data.s3.amazonaws.com/ZlGWYN_4nw2_QCNBBze9NTeHAoKfrvrhSLZVTQ46k4wn-rdMUkKQw3mxwKEW6LKKhz-1jOGi1vF1MiwP2R7gD8DF_RVObYXEmb5QacajdT7x1p4QkHoMoBIb3sF22rBT.png)
- Reducing the functionality in software reduces its attack surface area.
- Need to find the balance between functionality and usability for optimal security.
- Varies on a case by case basis, can find the sweet spot by communicating with customers, testing and prototyping.
![Balance](https://remnote-user-data.s3.amazonaws.com/P8xwmKnnB5svZqpS5NbTRdkUVTvvz8Vz8IsmM8JucWYlkU_6YNzHAk8fconWe-3RbbFNlSkoO_LGDO-uhmfRp5ukXX9JVPtftHff-mPcHZABLjnPe4m8dWCMCfo_8-30.png)

### Vulnerability
- The weakness that enables a threat to be successful.

### Threat
- A circumstance or event that could damage the confidentiality, integrity or availability of information or information systems.

## Cloud Vulnerabilities
### Example Threat Analysis
![Example Threat Analysis](https://remnote-user-data.s3.amazonaws.com/X-PwtkZZcnLkeEoUpLanKImnFzdm08JFqxGNv55X3mCE0B8oS8Ql4vif6P0yi_T2jy5hbuo40mglNeQeuU9FNw0S-7rQFKhpnXmWvv29B0QH-6gJMWwOfCbOhhFLJAeV.png)

### Supply Chain Risks
![Supply Chain Risks](https://remnote-user-data.s3.amazonaws.com/xOlHyulgGw8jIvD6l__qnpIqbEMWu3mYS6NaSBvQQFyNgKf26SbeZ3nmtui6BJwxyqEBnzuu_9KE-CkjXhzgr3eiPUmM46iAvN5p7UXIeOGAbFXZoSm2uhz6C3L39l11.png)

### Summary of Cloud Computing Threats
- Incident analysis and forensic support
- Business continuity and resiliency
- Regulatory compliance
- Infrastructure security
- User privacy and secondary usage of data
- Non-production environment exposure
- User identity federation
- Accountability and data ownership
- Multi-tenancy and physical security
- Service and data integration

### Accountability and Data Ownership
![Accountability and Data Ownership](https://remnote-user-data.s3.amazonaws.com/3oNU4fk41w-izJch0npAP31kW96bsbpwMo31-IC8PnszCeVtgJpifhj2Qo6sHYl9Js0W5Ydz_LoyAcENN7mUB8GT4IK3zIJfeY3__sy-HdYFXTJPzRLdikhwOQmhrC7S.png)
#### Things to consider
- Who owns the data
- How to encrypt it
- How to destroy it
- Where to store it (isolation _)
- Consider data toxicity

### User Identity Federation
- Identity providers
  - Open ID (Oauth)
  - SAML
  - Access Control Design
- One user identity can be used to login to multiple systems.
- Provides less control over user lifecycle.
- Improves user experience.
![User Identity Federation](https://remnote-user-data.s3.amazonaws.com/m5SGxJ_H4lLK-SD5cAuM_cByohXtjk3Lucw2vti_-eAjAm91ATs5GCQZJzYjAphSzOz9NEWd_2r9mvr-UknO3a4MWNJaFwBCidywxPxhxjx1o7nQQvE8WYbTIGXtQu8O.png)

### Regulatory Compliance
- Data perceived secure in one region is not assumed secure by another.
- Data stored in the US may not comply with EU law.
- Lack of transparency in the implementation makes it difficult for data owners to demonstrate compliance to owners.
- Lack of consistent global standard for handling data.
- Use a cloud vendor who understands and applies solutions for the various data protection laws.
  - They should also know how to handle cross-jurisdiction data protection requirements.

### Business Continuity and Resiliency
- Need to make sure that Security Level Agreements (SLAs) cover data resilience, protection, privacy and that the vendor has a robust disaster recovery process in place.

### User Privacy and Secondary Usage of Data
$$\begin{bmatrix}
\text{User Priority} & \text{Providers Priority}\\
\text{Keep personal data safe} & \text{Push out the liability to user via privacy and acceptable use policy}\\
&\text{Build additional services on user behaviour}\\
&\text{Do the minimum to achieve compliance}\\
&\text{Keep their social application more open}
\end{bmatrix}$$
#### Things you can do
- Encrypt storage
- Anonymise personal information
- Terms of service with providers

### Service and Data Integration
#### Data in Transit
- Authentication
- Authorization
- Accounting
- Protected using SSL/TLS
#### Data at Rest
- Protected using Encryption keys
- Confidentiality
- Integrity
- Availability

### Multi-tenancy and Physical Security
- Inadequate logical separations
- Co-mingled tenant data
- Malicious or ignorant tenants
- Shared service, single point of failure
- Uncoordinated change controls and misconfigurations
- Performance risks
#### Threats
- Side channel attacks
## Open Redirects
￼￼￼￼￼￼￼
​￼￼￼￼￼Reference Diagrams￼￼
​￼￼￼What categories do you need
####1. Define hosts - machines
####2. Define network - how connected together
####3. Define stakeholders - the people
​￼￼￼Basic reasoning
￼￼Reuse the diagram
￼￼Illustrate threats
￼￼Show impact on assets
￼￼Show impact on stakeholders
￼￼Manager infrastructure
​￼￼￼Advanced reasoning
￼￼Show forbidden relationships
￼￼Add monitoring nodes
￼￼Identify host assets that need to stretch
​￼￼￼Identify persistent assets
- 
​￼￼￼￼￼What is Policy￼￼ ↓ 
###1. ^^￼￼Network policy￼￼^^^^:^^  
###2. ‒you can measure
###3. ^^￼￼Code practise￼￼^^^^:^^  
###4. ‒If you are building
###5. ^^￼￼People Guidance￼￼^^^^:^^  
###6. ‒If you can't measure
- 
​￼￼￼Policy↔A statement that reflects the rules that everyone should abide by
- 
​￼￼￼￼￼Good policies are organized as follows￼￼ ↓ 
###1. Purpose
###2. Policy compliance
###3. Date tested
###4. Date updated
###5. Contact
- 
​￼￼￼￼￼Frameworks￼￼ ↓ 
###1. ^^￼￼Security Frameworks￼￼^^ 
###2. ‒We mean compliance, such as: 
###3. ‒‒^^ISO 27001^^ 
###4. ‒‒^^NIST^^ 
###5. ‒‒^^BSI ^^
###6. ^^￼￼Security Models￼￼^^  
###7. ‒We mean models, such as:
###8. ‒‒^^IoT^^ 
###9. ‒‒^^Blockchain^^ 
###10. ‒‒^^Cloud^^ 
- 
- 
​￼￼￼￼￼Measuring Security￼￼ ↓ 
###1. ^^The SANS Endpoint Security Maturity Model Curve^^
###2. Level 1:
###3. ‒Random, or Disorganised
###4. Level 2:
###5. ￼￼￼￼￼ - Scanning other tenants
- Cross-tenant attacks
- DoS
- Architecting for multi-tenancy
- Data encryption (per tenant)
- Controlled and coordinated change management
- Ability to audit the provider administrative access
- Third party assessment

### Incident Analysis and Forensic Support
- Cloud computing can make the forensic analysis of security incidents more difficult.
  - This is because audits and events may be logged to data centres across multiple jurisdictions.
- In the event of a data breach, you must understand how to identify and manage critical vulnerabilities so you respond to the incident as quickly and effectively as possible.
#### Investigator Teams
![Investigator Teams](https://remnote-user-data.s3.amazonaws.com/WKZpPq6K-mOC5PSnWsMoxGGhLwIIvAyiUHMS1MK-jVvvSuGKYCP1xKXqLEXAS9ahTCfRUkw18yHAihiVWDxJS_VX3G_OzFwncEwHcUHyae6ZY6y8nBLtNMSSuyAtM5Pr.png)
- Check your Cloud vendor policy on handling, evaluating and correlating event logs across jurisdictions.
  - Is there technologies in place, such as virtual machine imaging, to help in the forensic analysis of security incidents?

### Infrastructure Security
#### SANS Endpoint Security Maturity Model Curve
![SANS Endpoint Security Maturity Model Curve](https://remnote-user-data.s3.amazonaws.com/I_qx6clPu6FiguqHEBYgPBqYjo4cUMfL2lC37t_wAxjBsM5dI_pCvpSUyDY66oMS0nYJ9knUvlrK3V5TtV-GwTjqmTMHOVLi4OBFWp-Ihrkjl0-EKoXrHRKH_6uj6q62.png)
#### Cybersecurity Capability Maturity Model (C2M2)/Maturity Indicator Levels (MILs)
![C2M2/MILs](https://remnote-user-data.s3.amazonaws.com/K7CrYAK-dnLqiOYMwGMHDx7aErEeelYagNfAoNZxpz9oIffnchEhiWKNrVf15Kpp5avxYyg34aBHylapNHwe1MDyQs83vX60RcLPuPZygyQ59nI6hxLP_1KMtt01bUp1.png)

### Non-Production Environment Exposure
- Don't use the cloud to develop concepts or tests.
- Always use Multi-Factor Authentication.
- Treat any pre-production environment or data as top secret.
