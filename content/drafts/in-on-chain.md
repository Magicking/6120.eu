+++
title = "In on Chain"
date = "2023-01-29T02:30:51+01:00"
author = "Sylvain Laurent"
authorTwitter = "magicking_" #do not include @
cover = ""
tags = ["nft", "onchaingang"]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++



In-chain refers to something that is stored and processed on the blockchain, while on-chain refers to something that is stored on the blockchain but processed off-chain. In the case of NFT artwork, in-chain would refer to the media being processed to its final form by the first execution layer, such as the EVM in Ethereum. On-chain would refer to the media being stored on the blockchain, but the processing and rendering of the artwork happens off-chain using JavaScript, for example, in real-time.

Some media formats, such as SVG, contain multiple data streams that may require different levels of processing, it can be rendered using rasterization techniques, but it can also be enhanced with CSS and/or JavaScript. This means that some parts of the image may be processed in-chain, while others may be processed off-chain.

Additionally, depending on the context, the final form of the media may be different, it can be a raster image or a interactive vector image, so the processing can be different for each context and each final form. This can make it challenging to determine the appropriate level of in-chain and off-chain processing for certain types of media, and may require careful consideration of the specific requirements and constraints of the use case.

Thus we can define in-chain NFT  where the artwork does not require* turing complete processing post first on-chain execution (e.g: when tokenURI function return embbed audio/video in metadatas)
(as in mandatory). The processing capability being brought by the human user, and therefore, a NFT can be considered in-chain when it does not require post-chain processing, for example, in wallets, twitter profile pictures, and so on. On the other hand, NFTs that require Post-Chain Processing(PCP), for example, in browsers, desktop apps, or games, are considered on-chain NFTs.

Example of possible artwork media types with possible Post-Chain Processing:

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

Examples projects by media type:

Add OpenSea Link

In-chain BMP NFT is [Brotchain](https://etherscan.deth.net/address/0xd31fc221d2b0e0321c43e9f6824b26ebfff01d7d#code) NFT processing  image
In-chain WAV NFT is the [Bleeps](https://etherscan.deth.net/address/0xE114DCe59A333f8D351371F54188F92C287b73E6#code) NFT


(It's worth noting that the table is not an exhaustive list of all media types that can be used for NFT artwork)

The concept of in-chain and on-chain NFTs refers to the storage and processing of digital artwork on the blockchain by smart-contracts following NFT standards. In-chain NFTs are those where the artwork does not require Post-Chain Processing and can be viewed using standard software or hardware. On the other hand, on-chain NFTs require post-chain processing, such as in browsers or desktop apps. The broad spectrum of possibilities for In-chain NFTs allows for greater compatibility across devices and opens up unexplored possibilities for on-chain computation, such as the ability to create more interactive and dynamic artwork, or the ability to use smart contracts to create unique, one-of-a-kind pieces.

INSERT DIAGRAM from DRAW.IO

NB: We could use the [StarkNet Cairo CPU](https://arxiv.org/pdf/2109.14534.pdf) intercheangibly with the EVM as long as the smart-contract follows NFT standards.

More ressources:
 - [Simon de la Rouviere's Flavours of on-chain SVG blog post](https://blog.simondlr.com/posts/flavours-of-on-chain-svg-nfts-on-ethereum)