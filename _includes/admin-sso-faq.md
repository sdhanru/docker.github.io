<ul class="nav nav-tabs">
  <li class="active"><a data-toggle="tab" data-target="#tab1">General</a></li>
  <li><a data-toggle="tab" data-target="#tab2">SAML</a></li>
  <li><a data-toggle="tab" data-target="#tab3">Docker org and Docker ID</a></li>
  <li><a data-toggle="tab" data-target="#tab4">Identity providers</a></li>
  <li><a data-toggle="tab" data-target="#tab5">Domains</a></li>
  <li><a data-toggle="tab" data-target="#tab6">SSO enforcement</a></li>
  <li><a data-toggle="tab" data-target="#tab7">Managing users</a></li>
</ul>
<div class="tab-content">
<div id="tab1" class="tab-pane fade in active" markdown="1">

### Is Docker SSO available for all paid subscriptions?

Docker Single Sign-on (SSO) is only available with the Docker Business subscription. Upgrade your existing subscription to start using Docker SSO.

### How does Docker SSO work?

Docker Single Sign-on (SSO) allows users to authenticate using their identity providers (IdPs) to access Docker. Docker supports Azure AD and any SAML 2.0 identity providers. When you enable SSO, users are redirected to your provider’s authentication page to authenticate using their email and password.

### What SSO flows are supported by Docker?

Docker supports Service Provider Initiated (SP-initiated) SSO flow. This means users must sign in to Docker Hub or Docker Desktop to initiate the SSO authentication process.

### Where can I find detailed instructions on how to configure Docker SSO?

You first need to establish an SSO connection with your identity provider, and the company email domain needs to be verified prior to establishing an SSO connection for your users.

### Does Docker SSO support multi-factor authentication (MFA)?

When an organization uses SSO, MFA is determined on the IdP level, not on the Docker platform.

### Do I need a specific version of Docker Desktop for SSO?

Yes, all users in your organization must upgrade to Docker Desktop version 4.4.2 or later. Users on older versions of Docker Desktop will not be able to sign in after SSO is enforced, if the company domain email is used to sign in or as the primary email associated with an existing Docker account. Your users with existing accounts can't sign in with their username and password.

<hr>
</div>
<div id="tab2" class="tab-pane fade" markdown="1">

### Does SAML authentication require additional attributes?

You must provide an email address as an attribute to authenticate through SAML. The ‘Name’ attribute is optional.

### Does the application recognize the NameID/Unique Identifier in the SAMLResponse subject?

The preferred format is your email address, which should also be your Name ID.

### When you enforce SAML SSO, at what stage is the login required for tracking through SAML? At runtime or install time?

At runtime for Docker Desktop if it’s configured to require authentication to the organization.

### Do you have any information on how to use the Docker Desktop application in accordance with the SSO users we provide? How can we verify that we're handling the licensing correctly?

Verify that your users have downloaded the latest version of Docker Desktop. An enhancement in user management observability and capabilities will become available in the future.
<hr>
</div>
<div id="tab3" class="tab-pane fade" markdown="1">

### What’s a Docker ID? Can I retain my Docker ID when using SSO?

For a personal Docker ID, a user is the account owner, it’s associated with access to the user's repositories, images, assets. An end user can choose to have a company domain email on the Docker account, when enforcing SSO, the account is connected to the organization account. When enforcing SSO for an organization(s) or company, any user logging in without an existing account using verified company domain email will automatically have an account provisioned, and a new Docker ID created.

### What if the Docker ID I want for my organization or company is taken?

This depends on the state of the namespace, if trademark claims exist for the organization or company Docker ID, a manual flow for legal review is required.

### What if I want to create more than 3 organizations?

You can create multiple organizations or multiple teams under a single company. SSO is available at the company level.

<hr>
</div>
<div id="tab4" class="tab-pane fade" markdown="1">

### Is it possible to use more than one IdP with Docker SSO?

No. You can only configure Docker SSO to work with a single IdP. A domain can only be associated with a single IdP. Docker supports Azure AD and identity providers that support SAML 2.0.

### Is it possible to change my identity provider after configuring SSO?

Yes. You must delete your existing IdP configuration in Docker Hub and follow the instructions to Configure SSO using your IdP. If you had already turned on enforcement, you should turn off enforcement before updating the provider SSO connection.

### What information do I need from my identity providers to configure SSO?

To enable SSO in Docker, you need the following from your IdP:

* **SAML**: Entity ID, ACS URL, Single Logout URL and the public X.509 certificate

* **Azure AD**: Client ID, Client Secret, AD Domain.

### What happens if my existing certificate expires?

If your existing certificate has expired, you may need to contact your identity provider to retrieve a new x509 certificate. The new certificate must be updated in the SSO configuration settings page on Docker Hub.

### What happens if my IdP goes down when SSO is enabled?

It's not possible to access Docker Hub when your IdP is down. However, you can access Docker Hub images from the CLI using your Personal Access Token. Or, if you had an existing account before the SSO enforcement, you can use your username and password to access Docker Hub images during the grace period for your organization.

### What happens when I turn off SSO for my organization(s) or company?

When you turn off SSO, authentication through your Identity Provider isn't required to access Docker. Users may continue to sign in through Single Sign-On as well as Docker ID and password.

### Q: How do I handle accounts using Docker Hub as a secondary registry? Do I need a bot account?

You can add a bot account to your IDP and create an access token for it to replace the other credentials.

### Does Docker plan to release SAML just in time provisioning?

The SSO implementation is already "just in time". Admins don't have to create users’ accounts on Hub, they can just enable it on the IdP and have the users sign in through their domain email on Hub.

### Will there be IdP initiated logins? Does Docker plan to support SSO logins outside of Hub and Desktop?

We currently do not have any plans to enable IdP initiated logins.

### Build agents - For customers using SSO, do they need to create a bot account to fill a seat within the dockerorg?

Yes, bot accounts needs a seat, similar to a regular end user, having a non-aliased domain email enabled in the IdP and using a seat in Hub.

### Is it possible to connect Docker Hub directly with a Microsoft Azure Active Directory Group?

Yes, Azure AD is supported with SSO for Docker Business, both through a direct integration and through SAML.

<hr>
</div>
<div id="tab5" class="tab-pane fade" markdown="1">

### Can i add sub-domains?

Yes, you can add sub-domains to your SSO , however all email addresses should also be on that domain. Verify that your DNS provider supports multiple txt fields for the same domain.

### Can the DNS provider configure it once for one-time verification and remove it later OR will it be needed permanently?

They can do it one time to add it to a connection. If they ever change IdPs and have to set up SSO again, they will need to verify again.

### Is adding domain required to configure SSO? What domains should I be adding? And how do I add it?

Adding and verifying a domain is required to enable and enforce SSO. Select **Add Domain** and specify the email domains that's allowed to authenticate through your server. This should include all email domains users will use to access Docker. Public domains are not permitted, such as gmail.com, outlook.com, etc. Also, the email domain should be set as the primary email.

### If users are using their personal email, do they have to convert to using the Org’s domain before they can be invited to join an Org? Is this just a quick change in their Hub account?

No, they don't. Though they can add multiple emails to a Docker ID if they choose to. However, that email can only be used once across Docker. The other thing to note is that (as of January 2022) SSO will not work for multi domains as an MVP and it will not work for personal emails either.

### Since Docker ID is tracked from SAML, at what point is the login required to be tracked from SAML? Runtime or install time?

Runtime for Docker Desktop if they configure Docker Desktop to require authentication to their org.

### Do you support IdP-initiated authentication (e.g., Okta tile support)?

We don't support IdP-initiated authentication. Users must initiate login through Docker Desktop or Hub.


<hr>
</div>
<div id="tab6" class="tab-pane fade" markdown="1">

### We currently have a Docker Team subscription. How do we enable SSO?

SSO is available with a Docker Business subscription. To enable SSO, you must first upgrade your subscription to a Docker Business subscription. To learn how to upgrade your existing account, see [Upgrade your subscription](https://www.docker.com/pricing).

### How do service accounts work with SSO?

Service accounts work like any other user when SSO is turned on. If the service account is using an email for a domain with SSO turned on, it needs a PAT for CLI and API usage.

### Is DNS verification required to enable SSO?

Yes. You must verify a domain before using it with an SSO connection.

### Does Docker SSO support authenticating through the command line?

Yes. When SSO is enforced, you can access the Docker CLI through Personal Access Tokens (PATs).  Each user must create a PAT to access the CLI.

### How does SSO affect our automation systems and CI/CD pipelines?

Before enforcing SSO, you must create PATs for automation systems and CI/CD pipelines and use the tokens instead of a password.

### I have a user working on projects within Docker Desktop but authenticated with personal or no email. After they purchase Docker Business licenses, they will implement and enforce SSO through Okta to manage their users. When this user signs on SSO, is their work on DD compromised/impacted with the migration to the new account?

If they already have their organization email on their account, then it will be migrated to SSO.

### If an organization enables SSO, the owners can control Docker IDs associated with their work email domain. Some of these Docker IDs won't be users of Docker Desktop and therefore don't require a Business subscription. Can the owners choose which Docker IDs they add to their Docker org and get access to Business features? Is there a way to flag which of these Docker IDs are Docker Desktop users?

SSO enforcement will apply to any domain email user, and automatically add that user to the Docker Hub org that enables enforcement. The admin could remove users from the org manually, but those users wouldn't be able to authenticate if SSO is enforced.

### Can I enable SSO and hold off on the domain verification and enforcement options?

Yes, they can choose to not enforce, and users have the option to use either Docker ID (standard email/password) or email address (SSO) at the sign-in screen.

### SSO is enforced, but one of our users is connected to several organizations (and several email-addresses) and is able to bypass SSO and login through userid and password. Why is this happening?

They can bypass SSO if the email they're using to sign in doesn't match the organization email being used when SSO is enforced.

### Is there a way to test this functionality in a test tenant with Okta before going to production?

Yes, you can create a test organization. Companies can set up a new 5 seat Business plan on a new organization to test with (making sure to only enable SSO, not enforce it or all domain email users will be forced to sign in to that test tenant).

### Once we enable SSO for Docker Desktop, what's the impact to the flow for Build systems that use service accounts?

If SSO is enabled, there is no impact for now. We'll continue to support either username/password or personal access token sign-in.
However, if you **enforce** SSO:

* Service Account domain email addresses must be unaliased and enabled in their IdP
* Username/password and personal access token will still work (but only if they exist, which they won't for new accounts)
* Those who know the IdP credentials can sign in as that Service Account through SSO on Hub and create or change the personal access token for that service account.

<hr>
</div>
<div id="tab7" class="tab-pane fade" markdown="1">

### How do I manage users when using SSO?

Users are managed through organizations in Docker Hub. When you configure SSO in Docker, you need to make sure an account exists for each user in your IdP account. When a user signs in to Docker for the first time using their domain email address, they will be automatically added to the organization after a successful authentication.

### Do I need to manually add users to my organization?

No, you don’t need to manually add users to your organization in Docker Hub. You just need to make sure an account for your users exists in your IdP. When users sign in to Docker Hub, they're automatically assigned to the organization using their domain email address.

When a user signs into Docker for the first time using their domain email address, they will be automatically added to the organization after a successful authentication.

### Can users in my organization use different email addresses to authenticate through SSO?

During the SSO setup, you’ll have to specify the company email domains that are allowed to authenticate. All users in your organization must authenticate using the email domain specified during SSO setup. Some of your users may want to maintain a different account for their personal projects.

Users with a public domain email address will be added as guests.

### Can Docker org owners/Admins/company owners approve users to an organization and use a seat, rather than having them automatically added when SSO Is enabled?

Admins, organization owners and company owners can currently approve users by configuring their permissions through their IdP. That's if the user account is configured in the IdP, the user will be automatically added to the organization in Docker Hub as long as there’s an available seat.

### How will users be made aware that they're being made a part of a Docker Org?

When SSO is enabled, users will be prompted to authenticate through SSO the next time they try to sign in to Docker Hub or Docker Desktop. The system will see the end-user has a domain email associated with the docker ID they're trying to authenticate with, and prompts them to sign in with SSO email and credentials instead.

If users attempt to sign in through the CLI, they must authenticate using a personal access token (PAT).

### Is it possible to force users of Docker Desktop to authenticate, and/or authenticate using their company’s domain?

Yes. Admins can force users to authenticate with Docker Desktop by provisioning a `registry.json` configuration file. The `registry.json` file will force users to authenticate as a user that's configured in the `allowedOrgs` list in the `registry.json` file.

Once SSO enforcement is set up on their Docker Business organization or company on Hub, when the user is forced to authenticate with Docker Desktop, the SSO enforcement will also force users to authenticate through SSO with their IdP (instead of authenticating using their username and password).

Users may still be able to authenticate as a "guest" account using a non-domain email address. However, they can only authenticate as guests if that non-domain email was invited.

### Is it possible to convert existing users from non-SSO to SSO accounts?

Yes, you can convert existing users to an SSO account. To convert users from a non-SSO account:

* Ensure your users have a company domain email address and they have an account in your IdP
* Verify that all users have Docker Desktop version 4.4.2 or later installed on their machines
* Each user has created a PAT to replace their passwords to allow them to sign in through Docker CLI
* Confirm that all CI/CD pipelines automation systems have replaced their passwords with PATs.

### What impact can users expect once we start onboarding them to SSO accounts?

When SSO is enabled and enforced, your users just have to sign in using the email address and password.

### Is Docker SSO fully synced with Active Directory (AD)?

Docker doesn’t currently support a full sync with AD. That's, if a user leaves the organization, administrators must sign in to Docker Hub and manually remove the user from the organization.

Additionally, you can use our APIs to complete this process.

### What's the best way to provision the Docker Subscription without SSO?

Company or organisation owners can invite users through Docker Hub UI, by email address (for any user) or by Docker ID (assuming the user has created a user account on Hub already).

### If we add a user manually for the first time, can I register in the dashboard and will the user get an invitation link through email?

Yes, if the user is added through email address to an org, they will receive an email invite. If invited through Docker ID as an existing user instead, they'll be added to the organization automatically. A new invite flow will occur in the near future that will require an email invite (so the user can choose to opt out). If the org later sets up SSO for [zeiss.com](https://www.zeiss.com/) domain, the user will automatically be added to the domain SSO org next sign in which requires SSO auth with the identity provider (Hub login will automatically redirect to the identity provider).

### Can someone join an organization without an invitation? Is it possible to put specific users to an organization with existing email accounts?

Not without SSO. Joining requires an invite from a member of the Owners group. When SSO is enforced, then the domains verified through SSO will allow users to automatically join the organization the next time they sign in as a user that has a domain email assigned.

### When we send an invitation to the user, will the existing account be consolidated and retained?

Yes, the existing user account will join the organization with all assets retained.

### How can I view, update, and remove multiple email addresses for my users?

We only support one email per user on the Docker platform.

### How can I remove invitees to the org who haven't signed in?

They can go to the invitee list in the org view and remove them.

### How's the flow for service account authentication different from a UI user account?

It isn't; we don't differentiate the two in product.

<hr>
</div>
</div>









.




