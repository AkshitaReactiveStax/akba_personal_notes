
akshita2002bajaj15@gmail.com
KafkaKafka2112$$


| API Key    | 6ENAYR4JM3NPCEIV                                                 |
| API Secret | PoZC71BXEvkYOO7VMVXyvphLFfeDDOLdYpmrRIGouG1vD6cmJmIMST1CilO3/wYN 


confluent kafka client-config create java --api-key 6ENAYR4JM3NPCEIV --api-secret PoZC71BXEvkYOO7VMVXyvphLFfeDDOLdYpmrRIGouG1vD6cmJmIMST1CilO3/wYN
[WARN] Created client configuration file but Schema Registry is not fully configured.

Suggestions:
    Pass the `--schema-registry-api-key` and `--schema-registry-api-secret` flags to specify the Schema Registry API key and secret.
    Alternatively, you can configure Schema Registry manually in the client configuration file before using it.

# Required connection configs for Kafka producer, consumer, and admin
bootstrap.servers=pkc-619z3.us-east1.gcp.confluent.cloud:9092
security.protocol=SASL_SSL
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username='6ENAYR4JM3NPCEIV' password='PoZC71BXEvkYOO7VMVXyvphLFfeDDOLdYpmrRIGouG1vD6cmJmIMST1CilO3/wYN';
sasl.mechanism=PLAIN
# Required for correctness in Apache Kafka clients prior to 2.6
client.dns.lookup=use_all_dns_ips

# Best practice for higher availability in Apache Kafka clients prior to 3.0
session.timeout.ms=45000

# Best practice for Kafka producer to prevent data loss
acks=all

# Required connection configs for Confluent Cloud Schema Registry
schema.registry.url=https://psrc-j55zm.us-central1.gcp.confluent.cloud
basic.auth.credentials.source=USER_INFO
basic.auth.user.info=6WRNRMTGAX2LAPTP:MdsFxxpibsMCbsvpSUyd+O1xlui4gr4fUXHmJ3iTTvKMyPmIKupIpZKWncguv/Mr

schema registry id :
lsrc-773w9w

schema registry api key and secret 
 API Key    | 6WRNRMTGAX2LAPTP                                                 |
| API Secret | MdsFxxpibsMCbsvpSUyd+O1xlui4gr4fUXHmJ3iTTvKMyPmIKupIpZKWncguv/Mr 


----------------------------------------------------------

**##KafkaConfluentCliCommands** 
###   
Try it out!

Now that you have a cluster up and running in Confluent Cloud, you can administer using the [Confluent CLI](https://docs.confluent.io/confluent-cli/current/index.html?ajs_aid=490859b1-5cc1-4100-986e-d755093db9cd&ajs_uid=5490703).

---

##### 1. Install / Update the Confluent CLI

Run this command to install the Confluent CLI:

$ curl -sL --http1.1 https://cnfl.io/cli | sh -s -- latest

Copy

This script will install the CLI in ./bin by default. If you want to install it somewhere else, add the path to the end of the command and to your $PATH variable.Note: On Windows, you might need to install an appropriate Linux environment to have the curl and sh commands available, such as the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about). You can also download and install the [raw binaries](https://docs.confluent.io/confluent-cli/current/install.html?ajs_aid=490859b1-5cc1-4100-986e-d755093db9cd&ajs_uid=5490703#tarball-or-zip-installation).If already installed, update to the latest version with:

$ confluent update

Copy

##### 2. Log in to your Confluent Cloud organization using the Confluent CLI

Run this command to log in to the Confluent CLI:

$ confluent login --save

Copy

When prompted for your username and password, enter the same credentials that you used to log in to Confluent Cloud.The optional --save flag saves your login credentials to a local file for future use.

##### 3. Select your environment

Run this command to set your environment. To view the available environments, use the confluent environment list command.

$ confluent environment use env-y22gv6

Copy

##### 4. Select your cluster

Run this command to set your cluster. To view the available clusters, use the confluent kafka cluster list command.

$ confluent kafka cluster use lkc-n9z23z

Copy

##### 5. Use an API key and secret in the CLI

An API key is required to produce or consume to your topic. If you have an existing API key that you'd like to use, add it to the CLI with this command:

$ confluent api-key store --resource lkc-n9z23z

Copy

Key: <API_KEY>

Secret: <API_SECRET>

Otherwise, create a new API key and secret pair using this command:

$ confluent api-key create --resource lkc-n9z23z

Copy

Note: Save your API key and secret pair in a safe and secure place.After you have created or added your API key pair, copy the API key and paste it at the end of this command:

$ confluent api-key use <API_Key>

Copy

---

In order to complete the next steps, you will need permission to create a topic and read from and write to that topic. Learn more about permissions [here](https://docs.confluent.io/cloud/current/access-management/cloud-rbac.html?ajs_aid=490859b1-5cc1-4100-986e-d755093db9cd&ajs_uid=5490703).

##### 6. Create a topic

Run this command to create a topic named test-topic in your cluster:

$ confluent kafka topic create test-topic

Copy

Now, verify that your topic has been created:

$ confluent kafka topic list

Copy

##### 7. Produce messages to your topic

Now you're ready to produce and consume some messages.Run this command to start a console producer, which you can use to manually produce messages to test-topic

$ confluent kafka topic produce test-topic

Copy

Run that command, then produce a few messages to your cluster in Confluent Cloud using the console producer. You can do this by typing anything into the console and pressing Enter. For example:

$ confluent kafka topic produce test-topic

Copy

"test"

"test"

"foo"

"bar"

When you're done, press ctrl+C to exit the producer.

##### 8. Consume the messages you produced to your topic

To consume all of the messages in test-topic and print them to the console, run this command:

$ confluent kafka topic consume --from-beginning test-topic

Copy

To use a specific Consumer Group, append the following to the command: '--group YOUR_CONSUMER_GROUP_NAME'. If the Consumer Group does not already exist, one will be automatically created.Note: You can run the consume command in parallel with the produce command in different instances of the CLI. To try this, keep the consumer running, and open another terminal window. Then, in the new window, run the produce command from the previous step and produce some messages. You should see the messages being consumed in real time in the window where your consumer is running.Press ctrl+C to stop the consumer.

##### 9. Generate a client config

If you're ready to set up a producer or consumer, you can generate a config for the client using the CLI.

$ confluent kafka client-config create <LANGUAGE> --api-key <API_KEY> --api-secret <API_SECRET>

Copy

Supported languages:

- Java*
- Python*
- C#
- Node.js
- Spring Boot*
- Go
- C/C++
- REST API
- Scala
- Clojure
- Ruby
- Ktor*
- Rust
- Groovy

Learn more about creating clients [here](https://confluent.cloud/environments/env-y22gv6/clusters/lkc-n9z23z/clients/new).* These languages support [Schema Registry](https://confluent.cloud/environments/env-y22gv6/schema-registry) keys. Append  
--schema-registry-api-key <SR_KEY> and --schema-registry-api-secret <SR_SECRET> to the above command.