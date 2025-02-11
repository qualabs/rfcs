- Feature Name: cmcd_integration_to_videojs
- Start Date: 2023-07-17
- PR: (leave this empty)

# Summary
[summary]: #summary

This RFC proposes the implementation of Common Media Client Data (CMCD) support in the Video.js player. CMCD is a standardized approach for exchanging data between clients and content delivery networks (CDNs) to optimize content delivery and improve user experiences.

# Motivation
[motivation]: #motivation

The motivation behind adding CMCD support to video.js is to enable personalized video delivery and optimize the viewing experience for individual clients. CMCD allows CDNs to tailor video delivery parameters, such as bitrate, resolution, and buffer size, to specific client characteristics and network conditions. By including CMCD support, video.js can empower developers to provide adaptive video streaming experiences that adapt to each viewer's capabilities, resulting in improved video quality, reduced buffering, and optimized bandwidth usage.


## Goals
- Enable developers to easily enable or disable CMCD in the Video.js player.
- Provide an API for developers to set the Client ID (CID) and Session ID (SID) for CMCD.
- Support CMCD transmission through query parameters or headers, allowing flexibility based on CDN capabilities.


## Non-Goals
- This proposal does not aim to define the CMCD standard itself but rather to integrate it's support into video.js.
- It does not cover the implementation details of specific CDN's or how they handle CMCD data.


# Guide-level Explanation
[guide-level-explanation]: #guide-level-explanation

The implementation of CMCD support in the Video.js player introduces new concepts and functionalities that enable developers to optimize content delivery and enhance user experience.

### Enabling CMCD
Developers can easily enable CMCD in the Video.js player by utilizing the provided API. Here's an example:

#### 1. Enabling CMCD with Default Parameters:

```javascript
var options = {
  cmcd: true
};

var player = videojs('my-video-player', options);
```

In this example, the cmcd option is set to true without providing custom parameters. When cmcd is set to true, the Video.js player will utilize default parameters for CMCD, such as auto-generating a Session ID (SID) and using query parameters for CMCD transmission.

#### 2. Enabling CMCD with Custom Parameters:
```javascript
var options = {
  cmcd: {
    sid: 'session-id',
    cid: 'content-id',
    useHeaders: true
  }
};

var player = videojs('my-video-player', options);
```
In this example, the cmcd option is passed when initializing the Video.js player. By setting useHeaders to true, CMCD data will be transmitted through headers. Developers can also set the Content ID (CID) and Session ID (SID) to their desired values, such as 'content-id' and 'session-id', respectively.

### CMCD Transmission through Query Parameters or Headers

CMCD data can be transmitted to CDN's either through query parameters or headers, providing flexibility based on CDN capabilities. The examples above demonstrate the usage of headers by setting useHeaders to true. If useHeaders is set to false (or omitted), the CMCD data will be transmitted through query parameters instead.

Developers can choose the transmission method that aligns with their CDN requirements and implementation preferences.

### Content ID (CID) and Session ID (SID)

The Content ID (CID) is a unique identifier that represents the content being played. The Session ID (SID) is an identifier that represents a specific session or viewing session for the client.

Developers can set the CID and SID values according to their application requirements. It's important to ensure that these ID's are unique and persistent for each client or session.

For more information about CMCD and it's parameters, you can refer to the [ CTA-5004 Standard ](https://cdn.cta.tech/cta/media/media/resources/standards/pdfs/cta-5004-final.pdf).


# Reference-level explanation
[reference-level-explanation]: #reference-level-explanation

This is the technical portion. Explain the design in sufficient detail that:

* Its interaction with other features is clear.
* It is reasonably clear how the feature would be implemented.
* Corner cases are dissected by example.

The section should return to the examples given in the previous section, and explain more fully how the detailed proposal makes those examples work.

# Drawbacks
[drawbacks]: #drawbacks

Why should we *not* do this?

# Rationale and alternatives
[rationale-and-alternatives]: #rationale-and-alternatives

- Why is this design the best in the space of possible designs?
- What other designs have been considered and what is the rationale for not choosing them?
- What is the impact of not doing this?

# Prior art
[prior-art]: #prior-art

Discuss prior art, both the good and the bad, in relation to this proposal.
A few examples of what this can include are:

- Does this feature already exist in a player?
- Has this feature been discussed in a blog post, paper, or presentation?

This section is intended to encourage you as an author to think about the lessons from other players, and provide readers of your proposal with a fuller picture.
If there is no prior art, that is fine - your ideas are interesting to us whether they are brand new or if it is an adaptation from other languages.

# Unresolved questions
[unresolved-questions]: #unresolved-questions

- What parts of the design do you expect to resolve through the proposal process before this gets merged?
- What parts of the design do you expect to resolve through the implementation of this feature before stabilization?
- What related issues do you consider out of scope for this proposal that could be addressed in the future independently of the solution that comes out of this proposal?
