## PingCastle

When PingCastle is run, it generates an XML report. One of the options PingCastle offers, is to send this XML report to an API endpoint. This integration functions as that API endpoint - it listens for PingCastle reports and creates an incident for each report received.

### Configuring an instance
- The option `long running instance` must be selected - this allows the integration to run a "long-running" server to listen for reports.
- The parameter `longRunningPort` specifies the unique port on which the integration will listen. This port must not be used by any other instances or integrations.
- The parameter `API Key` is the Key __PingCastle__ must use when sending a report. This key must be generated by the user - a random string of at least 20 characters is recommended.

For more information about long-running integrations, check out the <~XSIAM>[Forward requests to long-running integrations](https://docs-cortex.paloaltonetworks.com/r/Cortex-XSIAM/Cortex-XSIAM-Administrator-Guide/Forward-Requests-to-Long-Running-Integrations) article.</~XSIAM> <~XSOAR_SAAS>Forward Requests to Long-Running Integrations article: [Cortex XSOAR 8 Cloud](https://docs-cortex.paloaltonetworks.com/r/Cortex-XSOAR/8/Cortex-XSOAR-Cloud-Documentation/Forward-Requests-to-Long-Running-Integrations) or [Cortex XSOAR 8 On-prem](https://docs-cortex.paloaltonetworks.com/r/Cortex-XSOAR/8.7/Cortex-XSOAR-On-prem-Documentation/Integration-commands-in-the-CLI) documentation.</~XSOAR_SAAS>


### Running PingCastle
#### This section explains how to run PingCastle in such a way that it sends its report to the integration.  
The basic PingCastle healthcheck when run on the Domain Controller command looks like this: `./PingCastle.exe --healthcheck`  
The options required for sending the report to a server are:
- `--api-endpoint http://example.com:port/` where `example.com` should be the URL of your Cortex XSOAR and `port` should be the port set as the `longRunningPort` in the instance settings.
- `--api-key apikey` where `apikey` is the API Key set in the instance settings.

At this point the command looks like this:  
`./PingCastle.exe --healthcheck --api-endpoint http://example.com:port/ --api-key apikey`

In order to run PingCastle from a remote computer add the following options:
- `--server url` where `url` is the url or the Domain Controller.
- `--user domain\username` where `domain` is the name of the domain and `user` is the username used to log in.
- `--password pass` where `pass` is the password used to log in. __This argument is optional and not recommended__ if it is not provided, PingCastle will prompt the user for a password when run.

At this point the full command looks like this:  
`./PingCastle.exe --healthcheck --server url --user domain\username --password pass --api-endpoint http://example.com:port/ --api-key apikey`

Or if the user would rather not put their password as plain text on the command line:  
`./PingCastle.exe --healthcheck --server url --user domain\username --api-endpoint http://example.com:port/ --api-key apikey`  
In this case PingCastle will prompt the user for the password when run.
