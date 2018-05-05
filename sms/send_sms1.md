### Send an SMS message
#### https://docs.microsoft.com/en-us/windows/uwp/contacts-and-calendar/sending-an-sms-message
##### As accessed May 5, 2018

##### This topic shows you how to launch the compose SMS dialog to allow the user to send an SMS message. You can pre-populate the fields of the SMS with data before showing the dialog. **The message will not be sent until the user taps the send button.**

##### To call this code, declare the chat, smsSend, and chatSystem capabilities in your package manifest. These are restricted capabilities but you can use them in your app. You need approval only if you intend to publish your app to the Store. See Account types, locations, and fees.

##### Launch the compose SMS dialog
##### Create a new ChatMessage object and set the data that you want to be pre-populated in the compose email dialog. Call ShowComposeSmsMessageAsync to show the dialog.



