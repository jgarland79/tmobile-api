T-Mobile API, developed in Java for accessing all your account information.

This is an unofficial API. This was developed by reverse engineering the T-Mobile client which is available on mobile platforms.

# Example #

```
public class TMobileClient {

    public static void main(String[] args) throws IOException {
        try {
            TMobile tmobile = TMobile.login("USERNAME", "PASSWORD");

            //Retrieve the user profiles (the mobile accounts you own)
            List<Profile> profiles = tmobile.getUserAccounts();

            for (Profile profile : profiles) {
                System.out.println(profile); //Print details

                //Retrieve the subscription details for each account
                List<Subscription> subscriptions = profile.getBillingAccount().getSubscriptions();

                for (Subscription subscription : subscriptions) {
                    //Get all the call records
                    List<CallRecord> callRecords = tmobile.getCallUsage(subscription);
                    for (CallRecord callRecord : callRecords) {
                        System.out.println(callRecord);
                    }

                    //Get all the entries related to data usage
                    List<DataRecord> dataRecords = tmobile.getDataUsage(subscription);
                    for (DataRecord data : dataRecords) {
                        System.out.println(data);
                    }
                }
            }

        } catch (IOException ex) {
            Logger.getLogger(App.class.getName()).log(Level.SEVERE, null, ex);
        }
    }
}

```