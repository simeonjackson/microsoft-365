<h1>Microsoft 365 Core Administration</h1>
<p>
I looked at On-premise Active Directory in a few of my other projects and wanted to dive into cloud-based management with Microsoft 365. This project focuses on user lifecycle management, basic email routing, and identity security baselines within the Microsoft ecosystem.

</p>
The objective was to simulate a real-world IT support scenario encompassing common Tier 1 requests like:

* onboarding new employees
* provisioning licenses
* securing accounts
* configuring shared resources
  
Executing these tasks across multiple Microsoft admin portals, the lab simulates day-to-day identity and access administration while enforcing fundamental security standards.
<br />

<h2>Environments and Technologies Used</h2>

* **Infrastructure:** Microsoft 365 Cloud Environment (Business Premium)
* **Management Portals:** Microsoft 365 Admin Center, Microsoft Entra Admin Center, Exchange Admin Center
* **Core Concepts:** Identity & Access Management (IAM), Cloud Licensing, Exchange Mail Flow, Multi-Factor Authentication (MFA), Troubleshooting & Account Provisioning


<h2>The Setup</h2>
<p>
  
To perform this lab, I spun up a fresh Microsoft 365 Business Premium trial tenant. This provided the necessary licensing to use Office web apps and the advanced security and identity features found within Microsoft Entra ID and Exchange Online.

<img width="1903" height="910" alt="Image" src="https://github.com/user-attachments/assets/96507f61-4133-46d8-8781-15630f4e31fa" />

</p>


<h2>Administrator Overview</h2>

I followed a basic scenario in this experiment acting as an IT Administrator handling an onboarding ticket. 

"A new sales employee and manager are joining. They need email access, multi-factor authentication, and access to shared sales resources."

I implemented the following:

* User & License Provisioning: Created standard user accounts and dedicated administrative accounts with precise licensing.

* Security Enforcement: Enabled Self-Service Password Reset (SSPR) and enforced MFA globally.

* Resource Sharing: Created a shared department mailbox and configured access delegation.

* Mail Flow Management: Set up automatic email forwarding rules.

* Break/Fix Troubleshooting: Simulated a licensing failure to observe and resolve the resulting loss of access.

Below I will go through the configuration and deployment of each requirement, verifying it works and explaining the objective behind the configuration.

<h2>Deployment and Configuration Steps</h2>

<h3>1. User Creation and License Assignment</h3>

In this scenario, I needed to create three accounts: John (Sales), Sarah (Manager), and a dedicated IT Admin account.

I navigated to the Microsoft 365 Admin Center > Active users and added the users. For John and Sarah, I assigned the Microsoft 365 Business Premium license to ensure they had access to cloud applications and email.

<img width="1917" height="912" alt="Image" src="https://github.com/user-attachments/assets/5a14122e-52c5-41f0-8b93-27e95e662fb8" />

<img width="1908" height="914" alt="Image" src="https://github.com/user-attachments/assets/acabc42e-d8ff-409d-b50f-c1261152a225" />

<img width="1913" height="914" alt="Image" src="https://github.com/user-attachments/assets/210dff90-f563-4447-a890-ed08acc51ac4" />

For the IT Admin account, I created the user without a product license, but assigned it the Global Administrator role. This follows the principle of least privilege and cost-efficiency—administrative accounts do not need an expensive Business Premium license just to manage the backend environment.

<img width="1917" height="916" alt="Image" src="https://github.com/user-attachments/assets/5cebba44-679f-4110-a824-fc532885960f" />

<img width="1875" height="922" alt="Image" src="https://github.com/user-attachments/assets/74915630-bc45-4504-962e-e6ace133d2b9" />


<h3>2. Enforcing Security Baselines (MFA & SSPR)</h3>

Relying on passwords alone is a massive security risk. To secure these new identities, I moved over to the Microsoft Entra Admin Center.

<img width="1867" height="933" alt="Image" src="https://github.com/user-attachments/assets/0af00a73-3447-46fb-9dcb-f857bb2543b0" />

First, under the left menu I selected Password Reset, I enabled Self-Service Password Reset (SSPR) for all users. This drastically reduces help desk tickets by allowing users to securely reset their own forgotten passwords without IT intervention.

<img width="1877" height="928" alt="Image" src="https://github.com/user-attachments/assets/539a35e6-1a6d-45f7-a403-b62dacf3547d" />

Next, under Conditional Access, I created a Tenant-wide policy forcing all users to register for Multi-Factor Authentication (MFA). This means that all users will have to have MFA set up on their devices to access resources from our organization.

<img width="1874" height="919" alt="Image" src="https://github.com/user-attachments/assets/2dbfacb9-edda-4cb0-8b60-c7c56c9013d7" />

To set this up, under Assignments, I chose to include all users and groups. And for target resources I chose All Resources to be included in the scope of this policy.

<img width="1572" height="880" alt="Image" src="https://github.com/user-attachments/assets/806373a3-a1a8-4ca4-89be-b81a66ec9b9d" />

<img width="1587" height="875" alt="Image" src="https://github.com/user-attachments/assets/faefb3ec-ca5d-40e3-83f3-967ab672f916" />

Then under the Access Controls option I selected Grant and clicked the radio button to Require multifactor authentication. This will require this control tp be implemented before granting access to resources for all users and groups specificied in this policy (all users in this case).

<img width="926" height="431" alt="Image" src="https://github.com/user-attachments/assets/c0811ff0-6973-4383-8d72-e0b6ee43429b" />

<h3>3. Creating a Shared Mailbox</h3>

Instead of customers emailing John or Sarah directly, the business requested a central "sales@" email address that both employees could access.

Back in the Microsoft 365 Admin Center, I navigated to Teams & groups > Shared mailboxes and created a new mailbox named sales@TechWithSimeon.onmicrosoft.com. Once created, I edited the mailbox members and granted both John and Sarah "Read and manage" access.

<img width="1872" height="923" alt="Image" src="https://github.com/user-attachments/assets/c003e556-8476-4bec-a034-d218f7e7b0aa" />

<img width="1876" height="923" alt="Image" src="https://github.com/user-attachments/assets/f055fc06-b1fa-485a-8590-53a153e41003" />

<img width="1874" height="924" alt="Image" src="https://github.com/user-attachments/assets/f9e4cfc5-b1f5-44a3-b59d-4bad458bc530" />

<img width="1878" height="926" alt="Image" src="https://github.com/user-attachments/assets/ef4ae9de-343c-462e-9a6d-f6542ec45e8d" />


To verify this, I logged into Outlook on the web as John. I right-clicked his folder list, selected "Add shared folder," and successfully opened the Sales inbox.

<img width="1912" height="909" alt="Image" src="https://github.com/user-attachments/assets/051bcde9-e31a-48b7-a207-d46d62e44016" />

<img width="1917" height="916" alt="Image" src="https://github.com/user-attachments/assets/6ad53335-8a9b-4b2f-abd0-fd335d1a494a" />

<img width="1912" height="916" alt="Image" src="https://github.com/user-attachments/assets/9f1bbb5d-75d6-41e7-9624-f3eb5315543f" />

<img width="1912" height="915" alt="Image" src="https://github.com/user-attachments/assets/c9f1f39c-83ee-489f-ba77-a7f6d8b740d5" />

I sent an email to the Sales inbox, and verified that I was able to access the email while logged in as John under the shared mailbox.

<img width="1870" height="922" alt="Image" src="https://github.com/user-attachments/assets/a03a6738-c5f3-4335-a33d-c5965aaab4de" />

<img width="1912" height="921" alt="Image" src="https://github.com/user-attachments/assets/16e1701f-ee76-41f7-a5d3-ff062b6b1ff9" />

<h3>4. Configuring Mail Forwarding</h3>

Next, simulating a scenario where an employee might be on leave, I configured mail forwarding to ensure that emails sent to Sarah were forwared to John's inbox..

Because this is a mail flow rule, I utilized the Exchange Admin Center. Under Mailboxes, I selected Sarah's account, navigated to the Mail flow settings, and enabled Email Forwarding, setting John as the forwarding recipient.

<img width="1867" height="925" alt="Image" src="https://github.com/user-attachments/assets/c45b959d-12f8-4c9f-bd03-84bc0d1ac165" />

<img width="1869" height="921" alt="Image" src="https://github.com/user-attachments/assets/54e9bcc7-e4ab-409f-9980-b8538a68ae89" />

<img width="1875" height="916" alt="Image" src="https://github.com/user-attachments/assets/549388d7-97ff-45fa-9238-17fa28861676" />

To test this, I logged in as my IT Admin account and sent a test email directly to Sarah. I then logged into John's account and verified that the email successfully arrived in her inbox.

<img width="1875" height="919" alt="Image" src="https://github.com/user-attachments/assets/bb7291b8-eaa7-4a84-9dec-d4af944aa256" />

<img width="1912" height="915" alt="Image" src="https://github.com/user-attachments/assets/ce9c7ac2-ee3c-419f-ad6e-56c09a576835" />


<h3>5. Break/Fix Simulation: Licensing Issues</h3>

Finally, I wanted to observe what happens when a user loses their license, which is a common cause of "missing email" tickets.

I went into the M365 Admin Center, selected John, and completely unchecked his Business Premium license. I then opened a private browsing window and attempted to log into his webmail. As expected, Microsoft threw an error stating that a mailbox could not be found for that user.

<img width="1875" height="924" alt="Image" src="https://github.com/user-attachments/assets/aa3d5802-8e59-446d-be6c-49068bb64216" />

<img width="1876" height="925" alt="Image" src="https://github.com/user-attachments/assets/a352d218-c375-449c-b6e8-b3c7b4a8a7e9" />

<img width="1441" height="829" alt="Image" src="https://github.com/user-attachments/assets/68edb466-ce17-4608-b570-539372a731e3" />

I returned to the Admin center, reapplied the license, and was able to successfully log in again, proving the direct tie between licensing and resource availability.

<img width="1873" height="922" alt="Image" src="https://github.com/user-attachments/assets/6aa550dc-12ce-44c6-9853-73c07e69ae86" />

<img width="1912" height="912" alt="Image" src="https://github.com/user-attachments/assets/90b1f86d-8b34-43fa-9eb8-d7b57686c973" />

<h2>Takeaways</h2>

<p>
This lab provided hands-on experience with the complete user lifecycle, moving beyond just creating an account. I learned that proper onboarding requires a clear understanding of license provisioning—assigning the exact tools a user needs while avoiding unnecessary costs (like leaving administrative accounts unlicensed). I also gained practical experience allocating shared resources, specifically setting up shared mailboxes and email forwarding, which are critical for department workflows and communication.

Most importantly, I learned how to navigate the segmented Microsoft ecosystem. Figuring out exactly where specific administrative tasks live was a major takeaway. I realized quickly that while basic user creation happens in the Microsoft 365 Admin Center, securing that identity happens in the Entra Admin Center, and managing their communication flows requires the Exchange Admin Center.

To document this learning process, I put together a separate, detailed breakdown of these admin centers on my tech blog which I have linked [here](https://techwithsimeon.io/microsoft-365-administration).
</p>
