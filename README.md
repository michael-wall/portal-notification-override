## Introduction ##
- A custom OSGi module to inject new template variable 'ctCollectionName' for use in Workflow Emails.
- Liferay DXP version: 2024.Q1.6
- The custom OSGi component TemplateNotificationMessageGenerator is used in place of the OOTB OSGi component TemplateNotificationMessageGenerator.
- The  OOTB OSGi component must be Blacklisted: com.liferay.portal.workflow.kaleo.runtime.internal.notification.TemplateNotificationMessageGenerator

## Notes ##
- This is a ‘proof of concept’ that is being provided ‘as is’ without any support coverage or warranty.
- The sharing of the 'proof of concept' is in no way an endorsement of this approach nor a recommendation to use this 'proof of concept'.
