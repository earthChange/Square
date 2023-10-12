# Square

See [Land-Plan](https://github.com/earthChange/Land-Plan)

----
Documentation from [box](https://github.com/functionland/go-fula/) follows:

## Architecture

`go-fula` is an implementation of the Fula protocol in Go (Golang). It is designed to facilitate smooth communication between clients and a mesh of backend devices (servers) and provide APIs for developers to build mobile-native decentralized applications (dApps).

A React Native app can communicate with servers using the `@functionland/react-native-fula` library, which abstracts the underlying protocols and `libp2p` connection and exposes APIs similar to those of MongoDB for data persistence and S3 for file storage.

Data is encrypted on the client side using [WebNative Filesystem (WNFS)](https://github.com/wnfs-wg/rs-wnfs) ( with bridges for [Android](https://github.com/functionland/wnfs-android) and [iOS](https://github.com/functionland/wnfs-ios) ). The encrypted Merkle DAG is then transferred to the blox server using Graphsync.

The **blox** stack can provide backup guarantees by having the data pinned on multiple servers owned by the user. In cases where absolute assurance of data longevity is required (e.g. password records in a password manager app or scans of sensitive documents), the cids of encrypted data can be sent to the [Fula blockchain](https://github.com/functionland/sugarfunge-node) and backed up by other blox owners, who are rewarded for their efforts.

By default, Libp2p connections are established through Functionland's libp2p relay over the internet or directly over LAN without the use of a relay.

## Packages

| Name | Description |
| --- | --- |
| [blox](blox) | Blox provides the backend to receive the DAG created by fulamobile and store it |
| [mobile](mobile) | Initiates a libp2p instance and interacts with WNFS (as its datastore) to encrypt the data and Send and receive files in a browser or an Android or iOS app. Available for [React-Native here](https://github.com/functionland/react-native-fula) and for [Android here](https://github.com/functionland/fula-build-aar) |
| [exchange](exchange) | Fula exchange protocol is responsible for the ctual transfer of data |

## Other related libraries

| Name | Description |
| --- | --- |
| [WNFS for Android](https://github.com/functionland/wnfs-android) | Android build for WNFS rust version |
| [WNFS for iOS](https://github.com/functionland/wnfs-ios) | iOS build for WNFS rust version |

## Run

```go
git clone https://github.com/functionland/go-fula.git

cd go-fula

go run ./cmd/blox --authorizer [PeerID of client allowed to write to the backend] --logLevel=[info/debug] --ipniPublisherDisabled=[true/false]
```

The default generated config goes to a YAML file in home directory, under /.fula/blox/config.yaml

## Build

```go
goreleaser --rm-dist --snapshot
```

## Build for the iOS platform (using gomobile)
This process includes some iOS specific preparation.
```sh
make fula-xcframework
```


## License

[MIT](LICENSE)

