+++
title = "{In,On}-Chain"
date = "2024-02-03T13:22:00+01:00"
author = "Magicking"
authorTwitter = "magicking_" #do not include @
cover = ""
tags = ["nft", "onchaingang"]
keywords = ["in-chain", "on-chain"]
description = "Discussion on the differences between in-chain and on-chain NFTs."
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

In-chain refers to data stored and processed on the blockchain, while on-chain relates to data stored on the blockchain but processed off-chain. In the case of NFT artwork, in-chain would refer to the media being processed in its displayable form by the first execution layer, such as the EVM in Ethereum. On-chain would refer to the media stored on the blockchain, but the processing and rendering of the artwork happens off-chain using JavaScript, for example, in real-time.

Some media formats, such as SVG, contain multiple data streams that may require different levels of processing; the primary data stream can be rendered using rasterization techniques and enhanced with CSS and JavaScript. Parts of the image may be processed in-chain, while others may be processed off-chain.

Depending on the context, the data type may be of multiple formats; it can be a raster image, an interactive vector image, or a sound so that the processing can be different for each context, and each processing layer may process it differently (EVM->JavaScript, Equalizer, ...).
Determining the appropriate in-chain and off-chain processing level for specific media types is challenging. It requires careful consideration of the particular requirements and constraints of the use case.

Thus, we can define in-chain NFT processing where the artwork does not require* turing complete processing after the first on-chain execution (e.g., when the tokenURI function returns embed audio/video/... in metadata)
(as in mandatory). The user's processing capability for observing an NFT from the blockchain resident source is in-chain when it does not require post-chain processing (e.g., Twitter PFP, Wallet, Browser, Smart-Watches, ...).
On the other hand, NFTs that require Post-Chain Processing (PCP), for example, in browsers, desktop apps, or games, are considered on-chain NFTs.

Media types with Post-Chain Processing:

| Media | Audio | Image | PCP |
| ----- | ------| ----- | ----|
|[AVI](https://en.wikipedia.org/wiki/Audio_Video_Interleave#) |X|X| |
|[BMP](https://en.wikipedia.org/wiki/BMP_file_format) | |X| |
|[GIF](https://en.wikipedia.org/wiki/GIF#File_format) | |X| |
|[GLB](https://en.wikipedia.org/wiki/GlTF#GLB) | |X| |
|[GLTF](https://www.khronos.org/assets/uploads/developers/library/overview/gltf-overview.pdf)| |X| |
|[JPG](https://en.wikipedia.org/wiki/JPEG#Syntax_and_structure) | |X| |
|[MP4](https://https://en.wikipedia.org/wiki/MP4_file_format#Data_streams) |X|X| |
|[WAV](https://en.wikipedia.org/wiki/WAV#) |X| | |
|[WebM](https://en.wikipedia.org/wiki/WebM#)|X|X| |
|[OGG](https://en.wikipedia.org/wiki/Ogg#) |X|X|[X](https://en.wikipedia.org/wiki/Continuous_Media_Markup_Language)|
|[HTML](https://en.wikipedia.org/wiki/HTML#)|X|X|X|
|[SVG](https://en.wikipedia.org/wiki/SVG) |X|X|[X](https://en.wikipedia.org/wiki/SVG_animation)|

## Example projects

In-chain BMP NFT is [ReaperGambitEpitaph](https://vscode.blockscan.com/ethereum/0x46d0d00e847ed9c2756cfd941e70d99e9152a22f) NFT processing image([Artwork](https://opensea.io/assets/ethereum/0x46d0d00e847ed9c2756cfd941e70d99e9152a22f/0))

In-chain WAV NFT is the [Bleeps](https://etherscan.deth.net/address/0xE114DCe59A333f8D351371F54188F92C287b73E6#code) NFT ([Artwork](https://opensea.io/assets/ethereum/0x9d27527ada2cf29fbdab2973cfa243845a08bd3f/405))


(This is not an exhaustive list of all media types used for NFT artworks)

The concept of in-chain and on-chain NFTs refers to storing and processing digital artwork within the blockchain context by smart contracts following NFT standards*.
In-chain NFT artworks do not require Post-Chain Processing; common standard hardware and software process them.
On-chain NFT artworks require post-chain processing, such as browsers or desktop apps. The broad spectrum of possibilities for In-chain NFTs allows for excellent compatibility across devices. It opens up unexplored possibilities for on-chain computation, such as creating more interactive and dynamic artwork or using smart contracts to create unique, one-of-a-kind pieces.

*and other forms.

## Mind map

<iframe frameborder="0" style="min-width:1024px; min-height:768px; width:1024px;height:768px;" src="https://viewer.diagrams.net/?target=blank&highlight=0000ff&nav=1&title=Dynamic%20NFT%20disambiguation.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1EKwLBN6kVsxHzujLLU3eX9c4ReQ2EUXX%26export%3Ddownload"></iframe>

More ressources:
 - [Simon de la Rouviere's Flavours of on-chain SVG blog post](https://blog.simondlr.com/posts/flavours-of-on-chain-svg-nfts-on-ethereum)