---
title: Token Gating Chat
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: token-gated-chat-room-tutorial
      title: Web SDK - Token Gated Chat Room Tutorial
    - type: link
      title: iOS Token Gated Chat Tutorial
      url: >-
        https://github.com/LiveLike/engagement-sample-app/wiki/Token-Gated-Chat-Tutorial
---
Token gating chats allows CMS operators to control which users can enter a chat based on specific criteria, such as Contract wallet address. The CMS operator can turn on the token gating at the creation of a new chat or when modifying chat room details. Gates can also be turned off in the same fashion. The default setting for chat rooms is token gating off. 

```text Swift
class SomeClass {
  let sdk: EngagementSDK
  
  func someMethod(){
    sdk.getChatRoomInfo(roomID: "<chat room id>") { result in
      switch result {
      case let .success(chatInfo):
          chatInfo.tokenGates.forEach { tokenGate in
            print("Contract Address: \(tokenGate.contractAddress)")
          }
      case let .failure(error):
          print("Error: \(error.localizedDescription)")
      }
    }
    }
}
```
```javascript JavaScript
//Get ChatRoom with token_gates
LiveLike.getTokenGatedChatRoomAccessDetails({
  roomId: "<room id>",
  walletAddress: "<user wallet address>"
}).then(({access, wallet_details, details}) => {
    console.log("chatroom access", access);
    console.log("wallet details", wallet_details);
    console.log("chatroom access detailed message", details);
});

//Add Listener to *chatroom-updated* event
LiveLike.addChatRoomEventListener(
    "chatroom-updated",
    listenerFn,
    { roomId }
);

//Remove listener to *chatroom-updated* event
LiveLike.removeChatRoomEventListener(
    "chatroom-updated",
    listenerFn,
    { roomId }
);
```
```Text Kotlin
var sdk: EngagementSDK
fun someMethod() {
    sdk.chat().getTokenGatedChatRoomAccessDetails("WALLET_ADDRESS",
                    "CHATROOM_ID", object :LiveLikeCallback<TokenGatingStatus>(){
                    
                        override fun onResponse(result: TokenGatingStatus?, error: String?) {
                            
                            result?.let {
                                if (result.access.name.equals(Access.allowed.name))
                                    println { "You are allowed to enter in to the Chat Room" }
                                else
                                    println { "You are not allowed to enter in to the Chat Room" }
                            }
                            error?.let {
                                println {error}
                            }
                        }
                    })
}
```
 What does gating a chat mean?

When an operator puts a gate on the chat, it means that only people with certain criteria can enter the chat room. The current accepted criteria is contract wallet address from NFTs.

# Why use a token gate?

Token gating a chat with an NFT allows certain users to enter a room because they have the proper contract wallet address. Users with this criteria can have access to otherwise private chat rooms. Adding a gate to a chat room allows for operators to determine who can be in the chat room or not. Based on implementation, you have the option to remove previous users or not if you add a gate to an already existing chat room. In the same sense, if you remove a gate from a chat the integrator has the control over if the chat history remains or is erased due to being previously gated. 

# How Token gating is used in LiveLike SDK

In LiveLike engagement SDK, producers can make the chat room token gated  
from the CMS by adding the tokens required to enter the chat room. Now, When  
integrators fetch chat room details they receive a property **token_gates **in the chat  
room details which is a list that contains the required contract addresses and their  
network types to access the chat room.  
Integrator would be required to connect the user's crypto wallet which will be  
required by the SDK’s API to know whether he/she owns the required token to access  
the chat room.

The integrators are exposed to the API **getTokenGatedChatRoomAccessDetails **which  
takes chat room id and crypto Wallet address as input and provides information whether  
he can access the chat room or not, along with detailed information about contract  
balances. It is up to the integrator how he fetches the user’s crypto wallet address.  
Based on the response we can let the user access the chat room or otherwise show him  
the detailed message.  
The SDKs contain the **getTokenGatedChatRoomAccessDetails **method that  
internally fetches the room details from the BE by sending chat room id as a parameter  
in the get API call. The room details contains the token gating information if the room is  
token gated. If the room is token gated then SDK fetches the wallet details by sending  
chat room id and wallet address to the BE, if wallet contains all the required tokens then  
he/she is allowed to enter the room.

The Blast BE is responsible for all the web3 operations, communicating with the  
blockchain network, fetching the crypto wallet balance, providing detailed response to  
the SDK calls & creating token gated chat rooms.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d276ea9-LiveLike_Flow.png",
        null,
        null
      ],
      "align": "center"
    }
  ]
}
[/block]

## CMS UI

![](https://files.readme.io/b5a30ac-Screen_Shot_2022-04-29_at_3.00.39_PM.png "Screen Shot 2022-04-29 at 3.00.39 PM.png")

## Add Token Gated Chat Room from CMS

Before creating token gated chat room we need to set up RPC URL on CMS  
Setting Up RPC URL

For Setting up RPC url for network type need to follow following steps

1. Go to My Organization.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/f0e6177-My_Organization.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

You will see something like this. With all the applications under Organisation.

2. Select the Application for which you want to update the RPC network URL.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/fc89268-apps.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

And you will be redirected to a page like this where on scrolling down you will see predefined  RPC for all network types and you can update it.

3. On Scrolling Down

All the Pre-defined RPC urls are visible which are updatable to connect with contract of that respective network type.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/2f6cfd6-urls.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

Now we can proceed to create chat room

4. Click on Chat Room from the left bar list.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/17c2771-chat_rooms.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

5. Create a new chat room from button New Chat Room.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/07e155e-new_chat_room.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

It will open a new modal for chat room details.

7. Switch On Token Gate Access’s  toggle button to add token gates.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/57fe2d9-token_gate.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

For adding a token gate you will need to add a valid contract address and its network type.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/d8eee04-token_gate_.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

You always have the privilege to add multiple contracts and the User will be needed to have tokens of all the contracts to access this chat.

And after clicking the Create button it will create a chat room with token gate.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/bb68022-created_room.png",
        null,
        ""
      ],
      "align": "center"
    }
  ]
}
[/block]

# Add Token Gated Chat Room from SDK

Besides adding the token gating to the chat room from the CMS, we can also add the  
token gating to the chat room from the SDKs.  
Here is how we can create a token gated chat room using Android SDK.  
Users can create a chat room with an optional title, optional visibility and optional list of  
ChatRoomTokenGate objects.  
**Parameters**: Title(Optional) , Visibility(Optional,Default value: everyone),  
tokenGates(Optional,Default value: null)  
**Response**: ChatRoomInfo Object, it contains the newly created chatroom Id, title & token gate information if available.

```javascript

func someMethod() {
	LiveLike.createChatRoom(title: "<chat room title>", visibility: .members,
		tokenGates: [{
		token_type: BlockchainTokenType.FUNGIBLE,
		network_type: BlockchainNetworkType.ETHEREUM,
		contract_address: 'contract_address'
		}]).then((chatRoom) => {
			console.log('newly created chat room', chatRoom);
		}).catch((error) => {
			console.error(error);
		})
}


```
```swift

class SomeClass {
	let sdk: EngagementSDK
		func someMethod() {
			sdk.createChatRoom(title: "<chat room title>", visibility: .members,
			tokenGates: [TokenGate]?) {
				result in
			switch result {
				case let .success(chatRoomID):
					print("Chat Room Id: \(chatRoomID)")
				case let .failure(error):
					print("Error: \(error.localizedDescription)")
			}
		}
	}
}

```
```kotlin

sdk.chat().createChatRoom(
	title, Visibility.everyone,
	object : LiveLikeCallback<ChatRoomInfo>() {
		override fun onResponse(result: ChatRoomInfo?, error: String?) {
			val response = when {
 			 result != null -> "${result.title ?: "NoTitle"}(${result.id})"
			else -> error
			}
			response?.let { it1 -> showToast(it1) }
		}
}, tokenGates)
```

Here, tokenGates is a list of ChatRoomTokenGate in Android and in iOS TokenGate objects.  
ChatRoomTokenGate/TokenGate includes contract address, network type, token type, attributes  
(traits) as fields.

The ChatRoomTokenGate object contains 4 fields:

**Contract Address**: The smart contract address for the token.  
**Token Type**: The type of token fungible or non fungible.  
**Network Type**: The blockchain network ie Ethereum, Chiliz, Hedera, Polygon.  
**Attributes**: The list of metadata of tokens.

# Sample use cases\*

\*These are just a few examples  
NFTs can be created and given for any reason. Therefore, their use to gate chats can be for a variety of reasons.  
For example, NFTs given to people in a specific location (like a field or arena) can enter a private chat together and discuss what is happening live.  
NFTs can be given to different wallet addresses for social media giveaways, such as a private chat with an athlete.  
Clients can partner with third party NFT distributors to create token chats based on points, features etc.

# Get Smart Contracts to Create Token Gated ChatRoom

In order to create token gated chat rooms we need to provide a list of contract addresses to `createChatRoom()`. For the ease of entering the contract addresses while creating the token gated chat room, SDKs provides an API `getSmartContracts() `to get all the saved contract addresses with their Aliases. Using these names instead of complex smart contract hexadecimal number users can easily create chat rooms.

```javascript

LiveLike.getSmartContracts().then((response)=>{  
  
		console.log("Paginated response for smart contract addresses details ")  
  
})


```
```swift

sdk.getSmartContracts(page: page) { result in
            switch result {
            case let .success(smartContractInfo):
                print("Contract names fetched")
            case let .failure(error):
                print("Error: \(error.localizedDescription)")
            }
        }

```
```kotlin

sdk.chat().getSmartContracts(
            pagination,
            object : LiveLikeCallback<List<SmartContractDetails>>() {
                override fun onResponse(result: List<SmartContractDetails>?, error: String?) {             
                   
                }
            })
            
```

# Token gating based on NFTs Metadata

NFT metadata refers to the additional information associated with a non-fungible token (NFT). It  
could be its creator, date or properties like color, size, style etc.  
We can create the chat room using metadata of NFTs by adding a list of attributes to the  
ChatRoomTokenGate object. The attributes object contains the trait name and trait value.  
**Attributes**  
           - Trait type  
           - value  
NFTs with these metadata are then checked in the wallet at the time of entering the chat room  
using **getTokenGatedChatRoomAccessDetails** method.