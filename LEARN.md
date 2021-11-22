# Building a bank with Solidity that isnt a toy; For beginners
Welcome to the Solidity Joyride Quest. In this quest you will learn all about the basics of developing applications on Ethereum. We don’t require you to have any background on Ethereum development. If you’re a developer in any programming language and you’ve heard the terms Ethereum, Blockchain, Crypto Currencies etc. you should be good.

In this quest we’ll be developing a Personal Bank Account using Ethereum – where you can deposit money and earn interest. Guess what, this won’t be a toy product that won’t work in the real world. It will be something you can start deploying in the real world directly. You will quickly see how Ethereum & Solidity are so much easier to develop applications that involve transacting real money – unlike any traditional programming language you’d have seen. Solidity has some constructs and data structures built into it that makes building financial applications simple and secure. By the end of this quest you’ll be able to deploy a bank that can start transacting real money.

Banks are some of the most sophisticated softwares to build because of how much security is needed. Using solidity, you’ll be able to write a secure bank that is as secure as the most secure bank on the planet with less than 30 lines of code.

Ethereum is the underlying blockchain infrastructure, and Solidity is a programming language to write applications.

At the end of this quest you’ll know how to build contracts that are almost as good as contracts written by projects like PoolTogether and Compound – which are multi billion dollar projects right now. There are multiple tracks you can pick from in later quests ranging from building your own DeFi projects, security auditing other contracts, and earn some money along the way!
## Remix
[https://remix.ethereum.org](https://remix.ethereum.org)

We will be writing all our code in a new IDE called Remix. It sucks, but it’s the best editor for Solidity available out of the box. It is a browser based IDE, so you don’t have to install any software to get started.

Remix is a code editor for Solidity. It also runs a toy blockchain that we’ll be using to deploy our first contract. Most of the steps are automated in Remix. In a later Quest, we’ll install all the components by hand to understand better what is happening under the hood.
## First contract (get contract balance)
[https://remix.ethereum.org/\#version=soljson-v0.8.4\+commit.c7e474f2.js&optimize=false&runs=200&gist=6df9936208ff26cffa24fb0ed60f3a2e&evmVersion=null](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=6df9936208ff26cffa24fb0ed60f3a2e&evmVersion=null)

This is the first contract.

a. First of all, mention license type. If you want to make source code open source, then write a commented line as the first line of solidity code.
// SPDX-License-Identifier: MIT

b. Also notice the first line “pragma”. This is basically a way to tell remix which version of solidity to use. Most programming languages encourage this, but aren’t required. But in solidity, it is required – because, the development of solidity is so fast that a new version is released almost every week and things keep breaking. To be sure, the solidity compiler version should be mentioned on the top of the file.

The next thing you’d notice is the keyword contract. Programs on solidity are called contracts. A contract keyword is exactly similar to the class keyword you would have encountered on js/py/java.

Lastly, the function that we’ve written in this class aka contract is to get account balance. It returns a uint – a slightly different syntax here.

This is one place where Solidity shines. A class can accept and store money natively – without having to integrate payment gateways like stripe or razorpay.

Every user and every program on Ethereum has an account. An account is identified by an address. It is unique for each account and looks something like “0x123123…”. This account can hold money. The little program we’ve written will also have an account by default. Whatever money we send to this account, the program is allowed to do whatever it wants with those funds. It can transfer it any other account, it can burn the money or it can just sit on that cash and do nothing. Using solidity, we can write the logic of how the program will use the money in the account.

We’ve not sent any money to our contract (aka program’s) account yet. But in the next few subquests, you’ll see how we can write the logic to receive money and use those funds to build a smart bank account.
## Compile, Deploy, Contract Address
Unlike JS/Py, solidity code needs to be compiled before it can be deployed or run. On the left bar, look for the compile button and hit “compile 1.sol”.

You might see some warnings, but that’s OK for now.

Once the compilation is successful, we’ll deploy it. Tap on the “deploy & transaction” button on the left sidebar.

Before we actually deploy this contract, we should look at a few concepts that are new to solidity and Ethereum.

On the top, you’ll see that there are a few accounts for you to choose from. Remix has automatically created 20 accounts for you and preloaded it with 100eth money. These accounts are identified by addresses, as we had seen earlier. Remix allows you to change accounts by choosing one from the dropdown.

I want you to notice that the account you’ve selected has 100Eth in it. This is because it costs some money to deploy a contract. So you need to select an account that actually has some Ethers in it. However these 100Eth are toy Ethers, available to use only within the Remix interface & only for testing.

Then, hit deploy. There are various other options on this screen, that we'll ignore for now. We'll come back to them in the next few quests.

Ethereum is a computer owned by everyone. Anyone can run code on that computer. We have to deploy code to be able to run on Ethereum. Anyone in the world can start calling the functions in the smart contracts that you've deployed immediately. You can even charge people for the same. Remix has an inbuilt toy version of Ethereum. Which is where we will be deploying first.

Now that you’ve deployed it, you’ll be able to start calling the functions.

On the right you’ll see a tick in the console box, meaning that it has been deployed and the balance of the selected account is now 99.99… This is because every deployment in Ethereum costs money. Every function call, costs money.

We will look at why it costs money in a later quest, because we need to understand how Ethereum works internally.

Now that the program has been deployed, an account has been created for this program where it can hold money. We can also start calling the functions we’ve written.

To interact with the contract you have just deployed, you can tap on the arrow next to the contract address on the left bar under deployed contracts and hit the button that corresponds to the function that we’ve written “getContractBalance”. Remix creates this UI with buttons and input boxes automatically, based on the content of the contract.

Each time you deploy a contract, it deploys a new instance. You cannot upgrade an already deployed contract by default. In a later quest we'll see how to overcome this limitation using upgradable contracts.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/e68cd379-d068-4f1f-95f3-6bc106c375c2.jpg)

When you hit the button and call the function, you’ll see the return in the output on the console on the bottom right. Make sure you tap on the expansion arrow next to “Debug” to see the entire log.

You have to look for “decoded_output” in these logs.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/5ee96bbc-28c1-41f0-962d-aad89f196e86.jpg)

It is zero right now because we’ve not sent any money to our contract. Let us now send some money in!
## Add money to contract
[https://remix.ethereum.org/\#version=soljson-v0.8.4\+commit.c7e474f2.js&optimize=false&runs=200&gist=845518edb7aba6f96cc863856fa1253b](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=845518edb7aba6f96cc863856fa1253b)

What would we have to do if we have to add some balance to a user? We’ll create a function that takes parameters address of the user who’s balance we want to update and a value of by how much.

That’s exactly what this function does here.

Let’s compile and deploy this.

Once it’s deployed tap on add balance, give an address, here’s a sample address for you 0x89Ce0f71D7387a580c6C07032f74f393a65d77F4 and a value say 1,000,000 to the call and hit transact.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/384dd7ea-72f4-4155-b9a8-4a536fada299.jpg)

After doing that tap the button getContractBalance. You’ll notice the output says 1M. But where did this balance come from? Did we just pull out a Million dollars from thin air? If money has come into this account, it must have gotten deducted from somewhere else, right?

To make sure this is a valid transaction, we need to add the following checks

1. Is the user calling this function allowed to update the account identified by the address in the parameter? What if someone sends calls this function with 0 as amount and overwirting a victim of all their life savings?
2. Does the user who is calling this function “addBalance” even have the amount of money they are looking add to the balance of the said account?
3. If yes (for the above), has the money been debited from some account before it is credited to the account of this smart contract?

This is a lot of mess, right? Ethereum let’s you bypass all of these checks. Let’s see how to write this code better in the next subquest.
## Add money to contract
[https://remix.ethereum.org/\#version=soljson-v0.8.4\+commit.c7e474f2.js&optimize=false&runs=200&gist=b69817e3901cd5e203c4ad37f170fae0&evmVersion=null](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=b69817e3901cd5e203c4ad37f170fae0&evmVersion=null)

In this code, we’ve added a function called addBalance

First thing to note is the keyword payable.

Typically, you only send parameters to a function call – on other programming languages.

On Solidity, you can send parameters AND money. To tell the compiler that this function is allowed to accept money – you add the modifier “payable”. If you have the payable keyword, you can start depositing money to this contract using this function.

How much money is being sent in this function call is denoted by the variable msg.value.

Who sent this message is denoted by msg.sender.

Msg is a special object that Ethereum attaches with every function call that’s made to a smart contract. Ethereum takes care of the user authentication under the hood. For now, Remix takes care of the authentication on your behalf - however, we will need to explicitly authenticate when calling functions in production. It authenticates who is calling the function and stores the address of the user that’s calling the function in msg.sender. If there is money being sent to the function call, Ethereum also guarantees that the sender actually holds those many ethers, and when they are sending ethers to this function, the money has been actually been deducted from their account. How Ethereum is able to do all this, we can safely ignore for this quest. We’ll dig into the machinery itself in a later quest.

When this function is called, we update the balance of that user, and the total amount being held by this contract.

We use mapping to store what is the balance of which user. A mapping is the same as the dictionary or map data structure you might know from other programming languages. While defining the mapping, we defined the key and value data types.

The key over here is an "address" of the user who will be depositing money to this smart account and the value is an integer (uint) denoting how much money has been deposited into this contract by this user.

We will be storing this information so that when they decide to withdraw it, we know how much money they’re entitled to withdraw.

We will also update the total amount being stored in this contract.

Next, lets compile and run a payable function.
## Payable value, msg.value, msg.sender v/s params, wei
Compile this program just like we did before & deploy it.

You’ll see that now there are two functions in the deployed contract. The payable function is of a different color from the one that we had written earlier. To call this function, we need to add some money. For that, pick an account from the drop down and pick how much money you want to send to the contract from this address in the box called “value” , choose ethers as the denomination.

![](https://qb-content-staging.s3.ap-south-1.amazonaws.com/public/fb231f7d-06af-4aff-bca3-fd51cb633f77/7e239380-c153-45fd-99cd-9f34b9fe83bb.jpg)

The number you entered in the “value” text box, is the amount of money you are going to send

You’ll see that there are 2 functions in this deployed contract. The function “addBalance” is of a different color – signifying it is payable. We can send money to this function. To do that find the input box “value” above the deploy button. Type in a value and select Ethers from the dropdown. This is how much money will be sent to the function call.

Now tap on the addBalance button in the contract.

When you see the tick in the console, you’ll also see that the balance has reduced from the account you chose. This is also when msg.value gets set. Ethereum takes care of the logistics like deducting the amount from your account and populating the msg object so that you as a developer don’t have to worry about it.

If you hit get contract balance now, you’ll see that it has now become non zero.

You’ll also notice that the number is much larger than the number of ethers you sent. That is because all transactions happen in the smallest possible denomination of ethers called wei. 1 wei = 10^-18 eth.

Now that we have money, how do we generate interest?

## introducing block, interest
[https://remix.ethereum.org/\#version=soljson-v0.8.4\+commit.c7e474f2.js&optimize=false&runs=200&gist=a89ad8b401426cb74656979d6dd6e58a&evmVersion=null](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=a89ad8b401426cb74656979d6dd6e58a&evmVersion=null)

When withdrawing, we not only want to give the money back, we also want to add some interest.

So we need to store when the deposit was made along with how much. For that we’ll introduce a new mapping called deposit timestamp.2

Now timestamps are tricky in solidity. There is no such thing as current timestamp. That is because, the functions you call on Ethereum/solidity aren’t executed immediately. They are batched into a few thousands. Once there are a few thousand function calls called transactions are registered, all of them are run together. This batch of function calls is called a block. The block in blockchain. A block is nothing but a set of all transactions that were a part of this batch. So we only get the timestamp of when the entire batch was run. i.e. block.timestamp = when were all the transactions in this block executed. That is why it takes between 10-20 seconds for a transaction to be completed on the real blockchain. Since we are using a toy blockchain, it appears to execute immediately.

Now that we have the timestamp stored of when the transaction was made to deposit money, we’ll add a function called getBalance. Here, the user address can be a parameter because we’ll let anyone look up any other person’s balance – but only the actual owner of the balance can withdraw it.

Let us in this function not only return the principal they deposited, but also a simple interest.

Note that the calculation looks a little complex because solidity doesn’t have support for decimals (float or double) yet.

Now that the interest has been calculated, let’s withdraw.
## withdraw, transfer
https://remix.ethereum.org/\#version=soljson-v0.8.7\+commit.e28d00a7.js&optimize=false&runs=200&gist=3555d7cca21a79acf36197d72e0c411f&evmVersion=null

Here we will allow for a withdrawal.

We need to look up what is the balance of the user who is requesting a withdrawal. So we will use msg.sender now just to make sure the withdrawal is being made by the person who is actually requesting the same.

We’ve already written how much money this user has including the simple interest. So we’ll just use the same function to get how much money to send to the withdrawer.

We need to send money to an account identified by an address. This address we know from msg.sender. But we’ll need to convert it into a payable address before we can send money. This is just a check to make sure we don’t send money to undeserving addresses by mistake. Then we initiate a transfer.

Let’s deploy.

This time after deploying, let’s add money to the account.

Check the balance a few times. We see that the balance is increasing, by whatever small amount.

Now let’s withdraw.

But you wouldn’t have received any amount back into your account. Why do you think that is? The transaction failed.

Let’s check balance in contract : 10eth

Let’s check the balance of the user : 10.0000001eth because of interest.

We've added a secret "\+1" to our get Balance, so that there is always some interest that is credited to your deposited amount, no matter how much time has passed! Free money!

Where is this interest coming from? Are we pulling it out of thin air? The contract can only send as much money it has in its coffers. We’re trying to send more than it has. So it fails.

We need to add money to the contract account itself.

So lets add that function, let’s compile and deploy again.

[https://remix.ethereum.org/\#version=soljson-v0.8.4\+commit.c7e474f2.js&optimize=false&runs=200&gist=9d52e6fb0e8b7ce89ba5c2bda4907ef9](https://remix.ethereum.org/#version=soljson-v0.8.4+commit.c7e474f2.js&optimize=false&runs=200&gist=9d52e6fb0e8b7ce89ba5c2bda4907ef9)

This time we will make sure we deposit money, fill up the account and only then withdraw money.

Awesome this time it works. You can see that the balance has increased in the account.

You have successfully written your first contract!

This is as good as any project out there that are generating billions of dollars in transactions!
## wait, what just happened?
You just successfully wrote code that runs on Ethereum. But how is it any different from running a python program on my desktop?

Ofcourse in this primer, we’ve abstracted out a lot of jargons so that we can get to the crux of the matter. To build resilient smart contracts, it is important to understand what is really happening and understand some of the jargons.

Ethereum is a world computer. Everyone is running code on this single computer. Anyone can connect their laptop to this world computer and add a CPU to it, and make it even more powerful. There are hundreds of thousands of computers that contribute their processing power to this world computer. Each of these computers are called miner nodes.

If you remember, it costed us some ethers to deploy a contract or call a function in our contract. That is because these miner nodes need to pay for electricity to keep their computers always on and connected to the world computer. This money we’re paying for running our code is called gas and it is paid in Ethers (or wei).

In the next quest we’ll explore more into these details and deploy what you’ve built so that you can start sharing the contract you’ve made with your friends 😊
