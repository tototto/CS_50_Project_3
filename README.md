# CS_50_Project_3_-Email-Client-Single-Page_Application-
Design a front-end for an email client that makes API calls to send and receive emails from the server that uses Django's Framework

The API, their usage and documentation for this project which this Web Based Front End Email Client Single Page Application is as per below:

## GET /emails/<int:email_id>

Sending a GET request to /emails/email_id where email_id is an integer id for an email will return a JSON representation of the email, like the below:

{
        "id": 100,
        "sender": "foo@example.com",
        "recipients": ["bar@example.com"],
        "subject": "Hello!",
        "body": "Hello, world!",
        "timestamp": "Jan 2 2020, 12:00 AM",
        "read": false,
        "archived": false
}

Sample Usage:

fetch('/emails/100')
.then(response => response.json())
.then(email => {
    // Print email
    console.log(email);

    // ... do something else with email ...
});

if the email doesn’t exist, or if the user does not have access to the email, the route instead return a 404 Not Found error with a JSON response of {"error": "Email not found."}.

## POST /emails

To send an email, send a POST request to the /emails route. The route requires three pieces of data to be submitted: a recipients value (a comma-separated string of all users to send an email to), a subject string, and a body string.

Sample Usage:

fetch('/emails', {
  method: 'POST',
  body: JSON.stringify({
      recipients: 'baz@example.com',
      subject: 'Meeting time',
      body: 'How about we meet tomorrow at 3pm?'
  })
})
.then(response => response.json())
.then(result => {
    // Print result
    console.log(result);
});

If the email is sent successfully, the route will respond with a 201 status code and a JSON response of {"message": "Email sent successfully."}.

Note that there must be at least one email recipient: if one isn’t provided, the route will instead respond with a 400 status code and a JSON response of {"error": "At least one recipient required."}. All recipients must also be valid users who have registered on this particular web application: if you try to send an email to baz@example.com but there is no user with that email address, you’ll get a JSON response of {"error": "User with email baz@example.com does not exist."}

## PUT /emails/<int:email_id>

This mark an email as read/unread or as archived/unarchived. 
To do so, send a PUT request (instead of a GET) request to /emails/<email_id> where email_id is the id of the email you’re trying to modify,

Sample Usage:

fetch('/emails/100', {
  method: 'PUT',
  body: JSON.stringify({
      archived: true
  })
})

The above sample would mark email number 100 as archived. The body of the PUT request could also be {archived: false} to unarchive the message, and likewise could be either {read: true} or read: false} to mark the email as read or unread, respectively.
