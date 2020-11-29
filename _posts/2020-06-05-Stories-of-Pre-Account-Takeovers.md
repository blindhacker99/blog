Hello Folks, this is Sourav. Hope you are doing well on the other side of the screen. I am a security enthusiast and bug bounty hunter from India. 
In this blog I will discuss some of my findings on Pre-Account Takeovers. 

So let's start without wasting much time :

> What is Pre-Account Takeover??

Pre-Account Takeover is a case of Account Takeover where the attacker has access to the victim's account prior to the victim's registartion and then the can observe the victim's 
actions on the account.

So one fine day I started testing the targets for Pre-Account takeovers. So the Pre-Account Takeovers we are discussing in this blog is due to "Improper Oauth Implementation"

![login](https://d2x3xhvgiqkx42.cloudfront.net/12345678-1234-1234-1234-1234567890ab/8769cf44-f342-494c-b25f-cc98c9da3e82/2019/05/27/104e9cab-2c11-4c10-8200-38f8ab3ff45c/0189b27a-abd2-4509-91dd-2e9715cbf3f5.png)


So you folks might have seen cases where :

1. The website is not verifying the email ID after registration.

2. The website is providing login via 3rd party applications like "Login with Google".

Now let's see two slightly different cases which I observed during in the wild - 

### Case 1 ###

In this case I am covering the websites which let you register an user account using your email ID and a password. 
And these websites also allow the user to login via 3rd party account like Google and Facebook. Pretty Simple Right?

Now What's Wrong??

The attacker can register an account with the victim's email ID and will wait for the victim to do login via any third party accounts like Google or Facebook. 
And when the victim visits the website and do login via 3rd party account like Google or Facebook than the website will merge both the accounts internally without letting the victims know that a account is alreay created with the same email ID.

And since the attacker already has access to the victim's account so this the case of Pre-Account takeover.


### Case 2 ###

In this case I am covering websites which lets you register using an mobile number, email ID and a password. The websites were properly verifying the mobile number by sending an OTP but the website is not verifying the email ID. 

Now in this case the attacker can create an account using his own mobile number and the victim's email ID. And when the victim will do login via any 3rd party account like Google or Facebook accounts than the website will merge both accounts internally based on the same email ID.


### Mitigations ###

Now let's discuss the mitigations which I have observed in the wild. 

1. The website verify the email ID.

2. If the victim is doing login via a 3rd party application and if an account is already registered with the same email ID than the website will ask the user to first link the 
    the 3rd party accounts.
    
3.  If the victim is doing login via 3rd party accounts and an account is already registered with the same email ID than the website will not terminate all the active session 
    disable the password which was intitially used to create an the account.
    
    
    
### Result



