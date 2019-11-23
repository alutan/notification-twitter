This service sends a tweet via the *@IBMStockTrader* account on **Twitter**.

This service expects a **JSON** object in the http body, containing the following fields: *id*, *owner*, *old*, and *new*.  It returns a **JSON** object containing the message sent (or any error message from the attempt) and the location (**Twitter**).

There is another implementation of this service called *notification-slack*, which posts the message to a **Slack** channel instead.  If both implmentations of the *Notification* service are installed, you could use **Istio** *routing rules* to determine which gets used, and under what conditions.

 ### Prerequisites for OCP Deployment
 This project requires three secrets: `jwt`, and `twitter`.
 
 ### Build and Deploy to OCP
To build `notification-twitter` clone this repo and run:
```
cd templates

oc create -f notification-twitter-liberty-deploy.yaml -n notification-twitter-liberty-dev
oc create -f notification-twitter-liberty-deploy.yaml -n notification-twitter-liberty-stage
oc create -f notification-twitter-liberty-deploy.yaml -n notification-twitter-liberty-prod

oc new-app notification-twitter-liberty-deploy -n notification-twitter-liberty-dev
oc new-app notification-twitter-liberty-deploy -n notification-twitter-liberty-stage
oc new-app notification-twitter-liberty-deploy -n notification-twitter-liberty-prod

oc create -f notification-twitter-liberty-build.yaml -n notification-twitter-liberty-build

oc new-app notification-twitter-liberty-build -n notification-twitter-liberty-build

```
