#### Challenge information

# Playlist Pandemonium

Disaster! Your absolute favorite playlist on the StreamWave music app, the legendary "Chill Lo-Fi Beats to Hack To", has been hit! Some tracks are just garbled noise, the titles are nonsensical, and your carefully crafted vibe is totally ruined. This smells like digital sabotage!

You were already monitoring your network traffic when things started sounding... strange. Luckily, you captured the data stream in `playlist_pandemonium.pcap` right when the corruption occurred. You suspect the notorious sound-scrambler, "DJ Distortion," is messing with your beats. They have a reputation for hiding messages in the most unusual ways. Maybe that garbled data isn't random noise after all?

#### Your Mission

Your goal is to analyze the provided network capture file (`playlist_pandemonium.pcap`) using Python. You need to:

1. Identify the specific network packets related to the playlist corruption.
2. Extract the hidden, encrypted data fragments (disguised as "lyrics") from these packets.
3. Determine the encryption method used and decrypt the fragments.
4. Combine the decrypted fragments in the correct order to reveal DJ Distortion's hidden signature tag.

This signature tag is the flag!

#### What you need to know

- The Python library `scapy`. You can usually install it via pip: `pip install scapy`.
- Basic knowledge of network protocols (UDP/IP) and packet structure.
- Basic knowledge of simple cryptographic ciphers.

## Hints

DJ Distortion isn't exactly subtle when they want to leave their mark. They seem to favor a specific, less common UDP port (`2468`) for their dirty work. The corrupted data fragments within the packets are marked with a specific prefix: `LYRIC:`. The encryption itself is a simple character-by-character substitution based on a short, repeating key – think XOR. The key is rumored to be related to music... maybe something like `BEAT`?


## Steps I took:
- Open the Pcap in wireshark
-  Filter packets by `udp.port == 2468 && frame contains "LYRIC:"`
-  select each packet and copy the data value 
   
![[challenge-how-to-wireshark.png]]
 - go to https://gchq.github.io/CyberChef/ and paste the data value removing everything before and including "3a" because that's the beginning ("LYRIC:" in Hex)
 - repeat for all packets in order
 - Recipe:
	 - Input: "From Hex"
	- Operation: "XOR" with key "BEAT" (can set to UTF-8)
![[challenge-recipe-rhythm.png]]**Final Answer: CTF{D3crypt_Th3_Rhythm}**