## Introduction ##
- When a Workflow is triggered from within a Publication, reviewers need to switch to the Publication to progress the Workflow Task. To do so they need to know the Publication to switch to.
  - The Publication Name is available from 2024.Q3 onwards, but isn't available out of the box in 2024.Q1.
  - https://learn.liferay.com/w/dxp/sites/publishing-tools/publications/collaborating-on-publications#configuring-invitation-email-notifications
- A custom OSGi module to inject new template variable 'ctCollectionName' for use in Workflow Emails where Publications is used.
  - ctCollectionId is available, the custom code uses ctCollectionId and _ctCollectionLocalServiceLocalService.fetchCTCollection to get the Publication record and it's name.
    - If the Workflow was triggered from Production mode then ${ctCollectionName} value is 'Production'. If the Publication can't be found the value is set to 'Unknown', otherwise it is the Publication name.
  - It can be used in the Notification Description field (i.e. the Email Subject) or in the Notification Template field (i.e. the Email Body) as follows:
    - ${userName} sent you a ${entryType} for review in Publication ${ctCollectionName}.
    - Sample output:
      - Roger Mellie sent you a Web Content Article for review in Publication mw test 101.
      - Roger Mellie sent you a Web Content Article for review in Publication Production.
  - If required, conditional logic based on ctCollectionId can be used within the FreeMarker template e.g. to exclude the additional text if ctCollectionId is 0 i.e. Production mode...
- The custom OSGi component TemplateNotificationMessageGenerator is used in place of the OOTB OSGi component TemplateNotificationMessageGenerator.
- The following OOTB OSGi component must be Blacklisted:
  - com.liferay.portal.workflow.kaleo.runtime.internal.notification.TemplateNotificationMessageGenerator

## Notes ##
- This is a ‘proof of concept’ that is being provided ‘as is’ without any support coverage or warranty.
- The sharing of the 'proof of concept' is in no way an endorsement of this approach nor a recommendation to use this 'proof of concept'.
- Smoke tested with 2024.Q1.6 and JDK 11.
- This approach is required as the TemplateContextContributor OSGi extension point is not applicable for Workflow Notification FreeMarker templates.
