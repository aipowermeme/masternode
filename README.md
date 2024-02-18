Install a masternode for your coin on Ubuntu Server 22.04 with the following tutorial.

Open your Windows wallet.

Go to Tools -> Debug console.

Type the following RPC command, to create an address for the masternode fee:

getnewaddress

Example output
AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque


Go back to your wallet overview.
Press on the toolbar button "Send".
Enter the address from the RPC command “getnewaddress” behind the text "Pay To:". (Example: AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque)


Enter the following amount of coins behind the text "Amount:": 5
Press on the button "Send".


Wait until the transaction is confirmed by 10 blocks.
Go back to the console of your wallet.


Type the following RPC command, to create an address for the masternode collateral:

getnewaddress

Example output
AHzQfVA4ANQkWwBkUvXBSFDQoXetAM6vEs



Go back to your wallet overview.
Press on the toolbar button "Send".
Enter the address from the RPC command “getnewaddress” behind the text "Pay To:". (Example: AHzQfVA4ANQkWwBkUvXBSFDQoXetAM6vEs)


Enter the following amount of coins behind the text "Amount:": 1000
Press on the button "Send".
Wait until the transaction is confirmed by 12 blocks.

Go back to the console of your wallet.

Identify the transaction with the following RPC command:

masternode outputs


Example output
{
 "a3d7e2fa6445c2fb3e6a5c01e654e2861ea0ae238f25e7200bff5adb247dfa48-1"
}



Generate a BLS key pair with the the following RPC command:
bls generate


Example output
{
 "secret": "0acbf6f183d0c9b794b9bc0dba25f8a1a1eca21aa4f2e4a86ecd3120a59efb35",
 "public": "064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9"
}



Type the following RPC command, to create an address for the owner of the masternode:
getnewaddress


Example output
APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE



Type the following RPC command, to create an address for used for proposal voting:
getnewaddress


Example output
AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM



Type the following RPC command, to create an address to receive the masternode reward:
getnewaddress


Example output
AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA




Prepare the ProRegTx transaction by modifying the following line.

protx register_prepare a3d7e2fa6445c2fb3e6a5c01e654e2861ea0ae238f25e7200bff5adb247dfa48 1 67.1.246.60:16100 APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE 064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9 AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM 0 AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque




fdab9dff1ff9caf5d291905ad43b9f7d69775189d4d22cb085d7fedd94ea1c6a - Transaction id from the RPC command “masternode outputs”.

1 - Single digit from the RPC command “masternode outputs”.

67.1.246.60:16100 - External IPv4 address of your VPS.

APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE - Address of the owner of the masternode.

064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9 - “public” value from the RPC command “bls generate”.

AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM - Address used for proposal voting.

AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA - Address to receive the masternode reward.

AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque - Address to where you send the masternode amount fee.


Paste the modified line into your console.

Example output


{
 "tx": "0300010001a55ee8d6ad1d5c1409a5328f4e53e80e3e7c83cf85253594141505fa64c5eeec0000000000feffffff0121dff505000000001976a9144f18fd993c0f9458fafb4985536dd358e9899a9f88ac00000000d10100000000006a1cea94ddfed785b02cd2d4895177697d9f3bd45a9091d2f5caf91fff9dabfd0000000000000000000000000000ffff88909c3714c4e172bd9c230db9cac3e446945cff2ea6720c2eca064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9b9772f1f7b0af05a67883806a4f60ddde4ecbf9e00001976a9143206f92dd6acc1a481cbb88fcadc19d0507bcb7d88ac0c5537044361500975adba10f9299f684f62a7f544e8e671638fee2c3914349f00",
 "collateralAddress": "AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque",
 "signMessage": "AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA|0|APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE|AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM|ac19e80b02d4e8a27feb42073114070a281a2b788ba064803e8064d259b22ebc"
}




Sign the ProRegTx transaction by modifying the following line.

signmessage "AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque" "AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA|0|APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE|AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM|ac19e80b02d4e8a27feb42073114070a281a2b788ba064803e8064d259b22ebc"



AWRC4W8ajZ23gZs9ooEgJp7MyQMAd5sque - “collateralAddress” value from the RPC command “protx register_prepare”.

AcY9DGdLK8egVrUBS9ipoexuFnmRNjQvdA|0|APVpUBhmUW1GaZhz1wCS5H4Y2RRFnZ8AcE|AX9yMNCKNcinGcdmrehcYbLsXwNUcGUmEM|ac19e80b02d4e8a27feb42073114070a281a2b788ba064803e8064d259b22ebc - “signMessage” value from the RPC command “protx register_prepare”.


Paste the modified line into the console of your wallet.


Example output
H/d9tkCSzqdYh8qLL1c+KDIlrb4vtFSfdxd88XDc3U/hRZ6lMuAR8TULy7vh1YXGk6AYFFV1xyPNuEdZVMN9SdI=



Submit the ProRegTx transaction by modifying the following line.


protx register_submit 0300010001a55ee8d6ad1d5c1409a5328f4e53e80e3e7c83cf85253594141505fa64c5eeec0000000000feffffff0121dff505000000001976a9144f18fd993c0f9458fafb4985536dd358e9899a9f88ac00000000d10100000000006a1cea94ddfed785b02cd2d4895177697d9f3bd45a9091d2f5caf91fff9dabfd0000000000000000000000000000ffff88909c3714c4e172bd9c230db9cac3e446945cff2ea6720c2eca064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9b9772f1f7b0af05a67883806a4f60ddde4ecbf9e00001976a9143206f92dd6acc1a481cbb88fcadc19d0507bcb7d88ac0c5537044361500975adba10f9299f684f62a7f544e8e671638fee2c3914349f00 H/d9tkCSzqdYh8qLL1c+KDIlrb4vtFSfdxd88XDc3U/hRZ6lMuAR8TULy7vh1YXGk6AYFFV1xyPNuEdZVMN9SdI=



0300010001a55ee8d6ad1d5c1409a5328f4e53e80e3e7c83cf85253594141505fa64c5eeec0000000000feffffff0121dff505000000001976a9144f18fd993c0f9458fafb4985536dd358e9899a9f88ac00000000d10100000000006a1cea94ddfed785b02cd2d4895177697d9f3bd45a9091d2f5caf91fff9dabfd0000000000000000000000000000ffff88909c3714c4e172bd9c230db9cac3e446945cff2ea6720c2eca064bb1741f4707cfe3629176857c41e0d23cbe751061fe5d0d67b506db10c8f3f6f2b684c3cec8e4a128193a001d12e9b9772f1f7b0af05a67883806a4f60ddde4ecbf9e00001976a9143206f92dd6acc1a481cbb88fcadc19d0507bcb7d88ac0c5537044361500975adba10f9299f684f62a7f544e8e671638fee2c3914349f00 - “tx” value from the RPC command “protx register_prepare”.


H/d9tkCSzqdYh8qLL1c+KDIlrb4vtFSfdxd88XDc3U/hRZ6lMuAR8TULy7vh1YXGk6AYFFV1xyPNuEdZVMN9SdI= - Output from the RPC command “signmessage”.


Paste the modified line into the console of your wallet.

Example output

7da2e1187202a1a497beca05e0e53a6e4df0dc06046f72fbf8b61c942db2982a



Open putty and connect using SSH with your Ubuntu server.
Update your Ubuntu server with the following command:
sudo apt-get update && sudo apt-get upgrade -y



Type the following command to go back to your home directory:
cd $HOME



Download the Linux daemon for your wallet with the following command:
wget "https://github.com/aipowermeme/masternode/releases/download/masternode/aipowermeme-daemon-linux.tar.gz" -O aipowermeme-daemon-linux.tar.gz



Extract the tar file with the following command:
tar -xzvf aipowermeme-daemon-linux.tar.gz



Download the Linux tools for your wallet with the following command:
wget "https://github.com/aipowermeme/masternode/releases/download/masternode/aipowermeme-qt-linux.tar.gz" -O aipowermeme-qt-linux.tar.gz



Extract the tar file with the following command:
tar -xzvf aipowermeme-qt-linux.tar.gz



Type the following command to install the daemon and tools for your wallet:
sudo mv aipowermemed aipowermeme-cli aipowermeme-tx /usr/bin/



Create the data directory for your coin with the following command:
mkdir $HOME/.aipowermeme



Open nano.
nano $HOME/.aipowermeme/aipowermeme.conf -t



Paste the following into nano.

rpcuser=rpc_aipowermeme

rpcpassword=dR2oBQ3K1zYMZQtJFZeAerhWxaJ5Lqeq9J2

rpcbind=127.0.0.1

rpcallowip=127.0.0.1

listen=1

server=1

daemon=1

maxconnections=125

masternode=1

masternodeblsprivkey=0acbf6f183d0c9b794b9bc0dba25f8a1a1eca21aa4f2e4a86ecd3120a59efb35

externalip=67.1.246.60




67.1.246.60 - External IPv4 address of your VPS.
0acbf6f183d0c9b794b9bc0dba25f8a1a1eca21aa4f2e4a86ecd3120a59efb35 - “secret” value from the RPC command “bls generate”.
Save the file with the keyboard shortcut ctrl + x.
Type the following command to start your masternode:
aipowermemed


