# About
The Corda Network Parameters Signer is a tool that can be used for create one of the most important crypto artifacts of a Corda Network, the Network Parameters. The Network Parameters is a crypto artifact that established the value of some network parameters, this crypto artefact should be accepted by all the nodes on a Corda Network, creating a consensus about the proposed parameters. The Network Parameters file should be signed by the network administrator and spread across all nodes. This tool create and sign the network parameters using the necessary files generated by the node or the java compiler, it is not necessary to create any file "by hand".

# Requirements
Please, see gradle related settings files.

# How to compile
Go to `./experimental/netparams` and execute `gradle build`.

# How to use
You can take a look to the comments in `./experimental/netparams/src/main/kotlin/net/corda/netparams/NetParams.kt`.

Open a terminal in the folder with the network parameter signer and execute: `java -jar netparams-4.8-SNAPSHOT.jar <commands>`.

The `commands` are:

`--config <path to config.json>`

Values for the Network Parameters are specified in a configuration file (in JSON format), an example content is shown below:

``` json
{
  notaries = [],
  minimumPlatformVersion = 1,
  maxMessageSize = 10485760,
  maxTransactionSize = 10485760,
  whitelistContracts = {},
  eventHorizonDays = 30,
  epoch = 1,
}
```

Please, do not fill `notaries` or `whitelistContracts` field, these fields should be filled using others commands.

`--notary-info <path to notary info file>`

If more than one notary exist the command should be repeated with the path of each one.

`--keystore <path to the keystore.jks>`

The path to the keystore file.

`--keystore-pass <key store password>`

The password of the keystore file.

`--keyalias <keyalias>`

The keyalias of the private key or the key pair.

`--keypass <key password>`

The password of the private key.

`--cordapps <path to the cordapps>`

The path to the cordapps wich contracts will be included in `whitelistContracts`. If more than one cordapp exist the command should be repeated with the path of each one.

`--output <name of the network parameter file>`

The name of the network parameter file.

Example command line: `java -jar netparams-4.8-SNAPSHOT.jar --config "./testnetparam.json" --notary-info "/home/ray/Documents/corda-network-aws/samples-java/Basic/ping-pong/build/nodes/Notary/nodeInfo-777DA369F066FE34BEDE3E6334A1006A4026A02DD76AFA798204BD015C9965DE"  --keystore /home/ray/Documents/corda-network-aws/cordadevcakeys.jks --keystore-pass cordacadevpass --keyalias netmap --keypass cordacadevkeypass --cordapps "/home/ray/Documents/corda-network-aws/samples-java/Basic/ping-pong/build/libs/ping-pong-1.0.jar" --cordapps "/home/ray/Documents/corda-network-aws/samples-java/Basic/ping-pong/build/nodes/Notary/cordapps/workflows-1.0.jar"  --output netparams -v
`
