<h1>Microsoft 365 Core Administration</h1>
<p>
Following the setup of a cloud-based tenant, this project focuses on user lifecycle management, basic email routing, and identity security baselines within the Microsoft ecosystem.

</p>
The objective was to simulate a real-world IT support scenario encompassing common Tier 1 requests like:

* onboarding new employees
* provisioning licenses
* securing accounts
* configuring shared resources
  
By successfully executing these tasks across multiple Microsoft admin portals, the lab demonstrates readiness to manage day-to-day identity and access administration while enforcing fundamental security standards.
<br />

<h2>Environments and Technologies Used</h2>

* **Infrastructure:** Microsoft 365 Cloud Environment (Business Premium)
* **Management Portals:** Microsoft 365 Admin Center, Microsoft Entra Admin Center, Exchange Admin Center
* **Core Concepts:** Identity & Access Management (IAM), Cloud Licensing, Exchange Mail Flow, Multi-Factor Authentication (MFA), Troubleshooting & Account Provisioning


<h2>The Setup</h2>
<p>
  
To perform this lab, I spun up a fresh Microsoft 365 Business Premium trial tenant. This provided the necessary licensing to use Office web apps and the advanced security and identity features found within Microsoft Entra ID and Exchange Online.
</p>


<h2>Administrator Overview</h2>

I followed a basic scenario in this experiment acring as an IT Administrator handling an onboarding ticket. 

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

For the IT Admin account, I created the user without a product license, but assigned it the Global Administrator role. This follows the principle of least privilege and cost-efficiency—administrative accounts do not need an expensive Business Premium license just to manage the backend environment.

[Insert Screenshot: Active Users list showing John and Sarah with licenses, and IT Admin without a license]


<h3>2. Enforcing Security Baselines (MFA & SSPR)</h3>

Relying on passwords alone is a massive security risk. To secure these new identities, I moved over to the Microsoft Entra Admin Center.

First, under Protection > Authentication methods, I enabled Self-Service Password Reset (SSPR) for all users. This drastically reduces help desk tickets by allowing users to securely reset their own forgotten passwords without IT intervention.

Next, under Identity > Properties, I enabled Security Defaults. This tenant-wide setting forces all users to register for Multi-Factor Authentication (MFA) within 14 days and requires it for all administrative access.

[Insert Screenshot: Security Defaults toggle set to Enabled in Entra ID]


<h3>3. Creating a Shared Mailbox</h3>

Instead of customers emailing John or Sarah directly, the business requested a central "sales@" email address that both employees could access.

Back in the Microsoft 365 Admin Center, I navigated to Teams & groups > Shared mailboxes and created a new mailbox named sales@mytenant.onmicrosoft.com. Once created, I edited the mailbox members and granted both John and Sarah "Read and manage" access.

To verify this, I logged into Outlook on the web as John. I right-clicked his folder list, selected "Add shared folder," and successfully opened the Sales inbox.

[Insert Screenshot: John's Outlook web view showing his personal inbox and the Shared Sales inbox beneath it]


<h3>4. Configuring Mail Forwarding</h3>

Next, I needed to ensure that any emails sent directly to John were also routed to his manager, Sarah.

Because this is a mail flow rule, I utilized the Exchange Admin Center. Under Mailboxes, I selected John's account, navigated to the Mail flow settings, and enabled Email Forwarding, setting Sarah as the forwarding recipient.

To test this, I logged in as my IT Admin account and sent a test email directly to John. I then logged into Sarah's account and verified that the email successfully arrived in her inbox.

[Insert Screenshot: Exchange Admin Center showing John's forwarding rules configured to send to Sarah]
(Note: If troubleshooting a failed forward, the Exchange Message Trace tool would be used to track the email's path through the server).


<h3>5. Break/Fix Simulation: Licensing Issues</h3>

Finally, I wanted to observe what happens when a user loses their license, which is a common cause of "missing email" tickets.

I went into the M365 Admin Center, selected John, and completely unchecked his Business Premium license. I then opened a private browsing window and attempted to log into his webmail. As expected, Microsoft threw an error stating that a mailbox could not be found for that user.

I returned to the Admin center, reapplied the license, and was able to successfully log in again, proving the direct tie between licensing and resource availability.

[Insert Screenshot: The Outlook error page showing "No mailbox found" alongside a split screen of John's license being removed]

<h2>Takeaways</h2>

<p>
This lab provided hands-on experience with the complete user lifecycle, moving beyond just creating an account. I learned that proper onboarding requires a clear understanding of license provisioning—assigning the exact tools a user needs while avoiding unnecessary costs (like leaving administrative accounts unlicensed). I also gained practical experience allocating shared resources, specifically setting up shared mailboxes and email forwarding, which are critical for department workflows and communication.

Most importantly, I learned how to navigate the segmented Microsoft ecosystem. Figuring out exactly where specific administrative tasks live was a major takeaway. I realized quickly that while basic user creation happens in the Microsoft 365 Admin Center, securing that identity happens in the Entra Admin Center, and managing their communication flows requires the Exchange Admin Center.

To document this learning process, I put together a separate, detailed breakdown of these admin centers on my tech blog which I have linked [here](https://github.com/simeonjackson/ad-troubleshooting).
</p>
