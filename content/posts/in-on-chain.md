+++
title = "{In,On}Chain discussion"
date = "2024-02-03T13:22:00+01:00"
author = "Magicking"
authorTwitter = "magicking_" #do not include @
cover = ""
tags = ["nft", "onchaingang", "in-chain", "on-chain", "inchain", "onchain"]
keywords = ["in-chain", "on-chain", "inchain", "onchain"]
description = "Discussion on the differences between inchain and onchain NFTs."
showFullContent = false
readingTime = true
hideComments = false
color = "" #color from the theme settings
+++

In the rapidly evolving realm of Non-Fungible Tokens (NFTs), distinguishing between "inchain" and "onchain" is crucial for understanding how digital artworks are stored and processed within the blockchain ecosystem. This article delves into the nuanced differences between these two concepts, shedding light on their implications for NFT artwork and its interaction with blockchain technology.

# Inchain vs. Onchain: Definitions and Distinctions
Inchain refers to data that is both stored and processed on the blockchain. When applied to NFT artwork, this means that the media is processed into its displayable form by the blockchain's first execution layer, such as the Ethereum Virtual Machine (EVM) for Ethereum. This process ensures that the artwork does not require Turing complete processing after the initial onchain execution, making it directly observable from the blockchain without additional postchain processing.

Onchain, in contrast, pertains to data that is stored on the blockchain but processed offchain. This means that while the media is stored within the blockchain, the actual rendering and processing of the artwork occur offchain, often in real-time and using external technologies like JavaScript. NFTs that necessitate such Postchain Processing (PCP) include those that are displayed or interacted with through browsers, desktop applications, or games.

## Challenges and Considerations
Selecting the appropriate level of inchain versus onchain processing for a specific media type involves navigating multiple challenges. These include considering the media's format (e.g., raster image, interactive vector image, sound) and the processing capabilities required at each layer (EVM to JavaScript, Equalizer, etc.). The decision hinges on the unique requirements and constraints of each use case, aiming to strike a balance between onchain storage efficiency and offchain processing flexibility.

Differentiating between pure SVG/HTML and Turing-complete languages highlights a conceptual challenge due to the inherent nature of SVG (Scalable Vector Graphics) and HTML (HyperText Markup Language) as descriptive languages, rather than computational or programming languages. SVG and HTML are fundamentally designed to describe the layout, structure, and presentation of content on the web, lacking the ability to perform arbitrary computations or algorithmic processes that define Turing completeness. This distinction becomes blurred when considering the interactive and dynamic capabilities that can be embedded within SVG and HTML documents through the use of JavaScript and CSS. While SVG and HTML alone do not possess the computational capabilities to be considered Turing complete, their integration with scripting languages enables them to support complex interactions and behaviors, making it difficult to separate their descriptive nature from the potential for Turing-complete operations facilitated by external scripts. This complexity underscores the challenge in categorizing SVG and HTML strictly as non-Turing-complete languages, especially in the context of modern web applications where the lines between content description and computational logic increasingly intersect.

## Media Types and Postchain Processing

The following table highlights various media types and their requirements for PostChain Processing (PCP):

Media types with Postchain Processing:

| Media | Audio | Image | PCP | Example | Comments |
| ----- | ------| ----- | ----| --------| ---------|
|[BMP](https://en.wikipedia.org/wiki/BMP_file_format) | |X| |[MoonBirds](https://opensea.io/fr/assets/ethereum/0x23581767a106ae21c074b2276d25e5c3e136a68b/8173), [ReaperGambitEpitaph](https://opensea.io/assets/ethereum/0x46d0d00e847ed9c2756cfd941e70d99e9152a22f/0) | Stored on Ethereum mainnet |
|[GIF](https://en.wikipedia.org/wiki/GIF#File_format) | |X| |n/a|n/a|
|[GLTF](https://www.khronos.org/assets/uploads/developers/library/overview/gltf-overview.pdf)| |X|?|[SkyLight](https://www.ord.io/489270)| Bitcoin Ordinal 489270 |
|[JPG](https://en.wikipedia.org/wiki/JPEG#Syntax_and_structure) | |X| |n/a|n/a|
|[MP4](https://https://en.wikipedia.org/wiki/MP4_file_format#Data_streams) |X|X|?|n/a|May contains multiple media streams|
|[WAV](https://en.wikipedia.org/wiki/WAV#) |X| | |[Bleeps](https://opensea.io/assets/ethereum/0x9d27527ada2cf29fbdab2973cfa243845a08bd3f/405)| Onchain sound note |
|[OGG](https://en.wikipedia.org/wiki/Ogg#) |X|X|[X](https://en.wikipedia.org/wiki/Continuous_Media_Markup_Language)|n/a|n/a|
|[HTML](https://en.wikipedia.org/wiki/HTML#)|X|X|X|[Yet Another Doom Clone](https://ordinals.com/content/521f8eccffa4c41a3a7728dd012ea5a4a02feed81f41159231251ecf1e5c79dai0)| Ordinal 466 |
|[SVG](https://en.wikipedia.org/wiki/SVG) |X|X|[X](https://en.wikipedia.org/wiki/SVG_animation)|n/a|n/a|


These examples underscore the versatility and potential of inchain NFTs for ensuring compatibility across various devices and platforms, opening new avenues for interactive and dynamic artwork creation via smart contracts.

# Costs

Inchain data insertion typically incurs lower costs compared to onchain methods due to the ability to leverage RPC provider execution to optimize the final artwork. The specifics of cost reduction may vary across different implementations. Additionally, storage maintenance is often provided at no additional cost on most blockchains.

Conversely, offchain storage solutions are significantly more cost-effective but require ongoing maintenance. Over an extended period, these maintenance expenses can accumulate, potentially surpassing the initial cost savings.

# Conclusion

The distinction between inchain and onchain NFTs lies at the heart of how digital artworks are stored, processed, and experienced within the blockchain framework. While inchain NFTs offer a seamless experience without the need for additional processing, onchain NFTs provide a canvas for more complex and interactive artworks, albeit with the requirement for external processing resources. As the NFT landscape continues to evolve, understanding these nuances becomes paramount for creators, collectors, and technologists alike.

## Future work - NFT Dynamism

NFT can be interactive and evolve, here is a mind map laying out the disambiugation work.

Click [here](https://viewer.diagrams.net/index.html?target=blank&highlight=0000ff&nav=1&title=Dynamic%20NFT%20disambiguation.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1EKwLBN6kVsxHzujLLU3eX9c4ReQ2EUXX%26export%3Ddownload) if you have trouble navigating the document.

<iframe frameborder="0" style="min-width:1024px; min-height:768px; width:1024px;height:768px;" src="https://viewer.diagrams.net/?target=blank&highlight=0000ff&nav=1&title=Dynamic%20NFT%20disambiguation.drawio#Uhttps%3A%2F%2Fdrive.google.com%2Fuc%3Fid%3D1EKwLBN6kVsxHzujLLU3eX9c4ReQ2EUXX%26export%3Ddownload"></iframe>

More ressources:
 - [On-Chain Checker](https://onchainchecker.xyz/)
 - [Simon de la Rouviere's Flavours of on-chain SVG blog post](https://blog.simondlr.com/posts/flavours-of-on-chain-svg-nfts-on-ethereum)
 - [Discover On-Chain NFT Projects](https://www.fullyonchain.art/)
