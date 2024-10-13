# Infrastructure as Code
 
## DevOps
### Development

- Developers
- Quality assurance
- Front end

### Operations

- Database admins
- Network admins
- System admins
 
## Combining Operations and Development

![|400](https://remnote-user-data.s3.amazonaws.com/2h1mhM8VRD5EfzUCNTgpYGRwmMLLAKAZrhqxBwGcqGXdNApgR4b11LhES7glKoLMDqPwkp3TyyEJbkYfPkKViPoKT_-hoOYtAb651CUz4_vTV5R85lDhvN2qylKLwDKU.png) 

## Infrastructure Creation

### Automatically Provisioned vs Manually Provisioned 

| **Automatically Provisioned**                                     | **Manually Provisioned**                                   |
| ----------------------------------------------------------------- | ---------------------------------------------------------- |
| Reduction in adding new bugs                                      | Introduces new bugs                                        |
| You can change it easily                                          | You cannot change it easily                                |
| Infrastructure can be relocated                                   | Infrastructure cannot be relocated                         |
| Infrastructure is written using a high-level programming language | Infrastructure is written using an operations manual       |
| One employee can manage a big infrastructure                      | A team may be needed to manage a small infrastructure      |
| Infrastructure is designed using code                             | Infrastructure is designed using graphs                    |
| Infrastructure can be tested and reviewed like code               | Infrastructure can be tested and reviewed after deployment |
| Development speed increases                                       | Slows development speed                                    |
| You can repeat it exactly                                         | You cannot repeat it exactly                               |

Artifact - What gets versioned, tested and deployed

Procedures (ala Imperative) -  An approach where the commands to produce a desired state are defined and executed 
- e.g. Bash script

Functions (aka Declarative) - Where you define the desired state and the tool conforms the system to the model of your desired state
- e.g. SQL queries, makefiles
 
## Service Delivery Platform
### Application

![|400](https://remnote-user-data.s3.amazonaws.com/-3NxAkOn7x79xIH8WiSmbj-y28Esakir9-y_892RZRu84KNCrwzsD7T_5ZL_7SFxCx_xTNW7Skb5uZvAXKf4qmWquorgQlw6c7RsrESJNojTMDwgFniT3LZdC6SQSImT.png) 

Typical application development scenario

### Infrastructure

![|400](https://remnote-user-data.s3.amazonaws.com/bZ4xNYF-AXj5gOI2kz3NZ_8ACjbXAmV6aX_KCMH3HX44jPGE5cW0EnS5Z_vb9Np2PpLU6iVKCObSFYJtiBkMs3Z4sJ9-aRQ7C48c_BxgCZ0FzHKj7OcCcjILRL2e3F1t.png)

### Tieing both Application and Infrastructure together

![|400](https://remnote-user-data.s3.amazonaws.com/1XQhcVPfRpmPgNz3dn7JsqFHJO46OxW93cgcvR8G57Igp-PjPbO57A_yoa9LLRsrr-YGc8Z09W-CWqkEitt_09N8FfOMC2gQINeVrNEoDlh_fSEHYb5woKVex8lnYLEE.png)

## Provision, Deployment, Orchestration and CM

Provisioning - The process of making a server ready for operation, including hardware, OS, system services and network connectivity

Deployment - The process of automatically deploying and upgrading applications on a server

Orchestration - The act of performing coordinated operations across multiple systems. Initial provisioning is done once and then the system runs for a long time, being able to control and upgrade a running system is critical

Configuration Management (CM) - The act of maintaining and upgrading application and application dependencies

![|400](https://remnote-user-data.s3.amazonaws.com/mUIgQUjTYUwMnHh3e7R-wAwBTiLmv22ssaPRKIbioCFp05i1m8TB0TePHtpfpxtX4oGzb4esfSj16OOPfhvHSZDFGw1fX5eeMX7TLBH4MtE-YHe5yLcZNqQosn14iDej.png) 
