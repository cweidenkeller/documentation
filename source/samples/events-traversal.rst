.. code-block:: bash

    curl -s --user 'api:YOUR_API_KEY' -G \
        https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/events

.. code-block:: java

 import javax.ws.rs.client.Client;
 import javax.ws.rs.client.ClientBuilder;
 import javax.ws.rs.client.Entity;
 import javax.ws.rs.client.WebTarget;

 import javax.ws.rs.core.Form;
 import javax.ws.rs.core.MediaType;

 import org.glassfish.jersey.client.authentication.HttpAuthenticationFeature;

 public class MGSample {

     // ...

     public static ClientResponse GetLogs() {

         Client client = ClientBuilder.newClient();
         client.register(HttpAuthenticationFeature.basic(
             "api",
             "YOUR_API_KEY"
         ));

         WebTarget mgRoot = client.target("https://api.mailgun.net/v2");

         return mgRoot
             .path("/{domain}/events")
             .resolveTemplate("domain", "YOUR_DOMAIN_NAME")
             .request()
             .buildGet()
             .invoke(ClientResponse.class);
     }
 }

.. code-block:: php

  # Include the Autoloader (see "Libraries" for install instructions)
  require 'vendor/autoload.php';
  use Mailgun\Mailgun;

  # Instantiate the client.
  $mgClient = new Mailgun('YOUR_API_KEY');
  $domain = 'YOUR_DOMAIN_NAME';

  # Make the call to the client.
  $result = $mgClient->get("$domain/events");

.. code-block:: py

 def get_logs():
     return requests.get(
         "https://api.mailgun.net/v3/YOUR_DOMAIN_NAME/events",
         auth=("api", "YOUR_API_KEY"))

.. code-block:: rb

 def get_logs
   RestClient.get "https://api:YOUR_API_KEY"\
   "@api.mailgun.net/v3/YOUR_DOMAIN_NAME/events"}
 end

.. code-block:: csharp

 using System;
 using System.IO;
 using RestSharp;
 using RestSharp.Authenticators;
 
 public class EventsTraversalChunk
 {
 
     public static void Main (string[] args)
     {
         Console.WriteLine (EventsTraversal ().Content.ToString ());
     }
 
     public static IRestResponse EventsTraversal ()
     {
         RestClient client = new RestClient ();
         client.BaseUrl = new Uri ("https://api.mailgun.net/v3");
         client.Authenticator =
             new HttpBasicAuthenticator ("api",
                                         "YOUR_API_KEY");
         RestRequest request = new RestRequest ();
         request.AddParameter ("domain", "YOUR_DOMAIN_NAME", ParameterType.UrlSegment);
         request.Resource = "{domain}/events";
         return client.Execute (request);
     }
 
 }

.. code-block:: go

 // coming soon
