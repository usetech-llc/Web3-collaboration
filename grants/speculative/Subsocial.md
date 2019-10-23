# Subsocial - SRML and UI for decentralized communities

## Project Description

**SubSocial** is a Substrate runtime module (SRML) with UI that allows anyone to launch their own decentralized censorship-resistant social network aka community. We are planning to follow a topology of Polkadot Network where every community will be running on its own Substrate chain and all these decentralized communities will be connected to our own Polkadot relay. This social networking relay could be connected to the official Polkadot Network.

You can think of this as decentralized versions of Reddit, Stack Exchange or Medium, where subreddits or communities of Stack Exchange or blogs on Medium run on their own chain. At the same time, users of these decentralized communities should be able to transfer or share their reputation, coins and other values from one community to another via Polkadot relay.

## Team Members

**Alex Siman** – Software Architect and Project Manager at Subsocial. Alex is a Polkadot Ambassador, a founder of “Polkadot Ukraine”, and a blockchain and UI developer at Joystream.org – a user-governed video platform built on top of Substrate. He has been building complex web apps since 2008. In 2017 he started to write smart contracts on Solidity and integrate them with dapps. Since 2019 he has been developing Substrate modules and building a custom UI for these modules by extending Polkadot Apps. Links: [GitHub](https://github.com/siman), [LinkedIn](https://www.linkedin.com/in/alexsiman/)

**Oleg** – Frontend Developer (TypeScript, React). Oleg develops UI for Subsocial using a fork of Polkadot.js Apps. His main contribution to this project can be found in UI repo:
https://github.com/dappforce/dappforce-subsocial-ui/commits?author=mell-old

**Vlad** – Backend Developer (Rust, C++). Vlad writes SRML and tests for Subsocial. His main contribution to this project can be found in Substrate runtime repo:
https://github.com/dappforce/dappforce-subsocial-runtime/commits?author=F3Joule

Both Oleg and Vlad are computer science students. Before the Subsocial project, they had a few side jobs in web projects as freelance developers. That’s why there is not so much to say about their production level experience in software development. In case we get the technical grant, we are about to hire one more skilled software developer.

**Hanna Yakimets** – Human Resources and Strategic Partnerships Manager. Hanna has a strong experience in international PR and media relations management. She has proficiency in organizing various events in innovation businesses about Europe, running IT schools, doing PR in Blockchain startups. Recently, in July 2019, she joined the Polkadot Ambassadors program.
Links: [LinkedIn](https://www.linkedin.com/in/anna-yakimets-61021a119)

## Team Website

https://github.com/dappforce

## Legal Structure

Sole Proprietorship based in Ukraine.

## Project Repos

The repo with SRML for Subsocial is based on a fork of Joystream’s runtime repo, that’s why several Joystream modules. In the future, we would like to split Subsocial it into separate modules so they could be used together or separately and applied to other SRMLs developed by third-parties. But right now, Subsocial SRML is in a single monolithic file:
https://github.com/dappforce/dappforce-subsocial-runtime/blob/df/src/blogs.rs

UI is built on a fork of Polkadot.js Apps as a custom module, that’s why it will be very familiar to those who already develop UI for Substrate using Polkadot Apps. The main React components of Subsocial can be found in the package called “df-blogs”:
https://github.com/dappforce/dappforce-subsocial-ui/tree/df/packages/df-blogs/src

The last repo is a Substrate node and it doesn’t include runtime modules because they are located in their own repo. The node repo is here:
https://github.com/dappforce/dappforce-subsocial-node

## Docker Containers

### Run node + runtime:

```sh
docker run -d -p 30333:30333 -p 9944:9944 -v ~/dappforce:/data dappforce/subsocial-node:df-pre-ipfs joystream-node --dev --ws-external
```

### Run web UI:

```sh
docker run --rm -itd -p 80:80 dappforce/subsocial-ui:df-pre-ipfs
```

Go to http://localhost

## License

GNU GPL v3.

## Development Roadmap

### Milestone 1 – IPFS integration, Edit history – 1 month – $10,000

#### IPFS integration:

Currently we store all text content onchain. And in this milestone we want to refactor Subsocial module to store text content of blogs, posts and comments on IPFS.

- Store blogs on IPFS (name, description, cover image, etc.).
- Store posts on IPFS (title, body, summary, tags, cover image, publishing date, etc.)
- Store comments on IPFS.
- Store public member profiles on IPFS (username, avatar, about, links to other social networks).

#### Edit history:

Store an edit history on IPFS + list of CIDs in Substrate storage in a corresponding struct: blog, post, comment or profile.

- Save and view an edit history of a post.
- Save and view an edit history of a blog.
- Save and view an edit history of a comment.
- Save and view an edit history of a member profile.

#### What to expect?

Users will be able to deploy a Substrate node and web UI that includes our modules. This will allow a user to send an extrinsic that let's them create a new blog, post or comment. A content of every new entity: name and description of a blog, title and body of a post, and a comment will be added to IPFS before extrinsic's sent to Substrate. A structure, ownership and IPFS CID of a new entity will be saved to Substrate storage.

A user should be able to edit any their entities (blog/post/comment). An updated content of an entity will be added to IPFS and the new CID will replace the current CID in a related structure of an entity in Substrate storage. All previous CIDs of every entity after it's updated by a user will be stored in a structure field called `edit_history`. A user should be able to view an edit history of an updated entity on web UI.

#### Documentation & Docker:

Both documentation and Docker containers should be updated to reflect new features and changes introduced in this milestone.

### Milestone 2 – Reputation, Activity stream – 1 month – $10,000

#### Rating and reputation:

- Update a comment rating after the comment upvoted/downvoted.
- Update a post rating after it has been upvoted/downvoted.
- Update a blog rating after its post has been upvoted/downvoted.
- Update an account/member reputation after their post/comment upvoted/downvoted.

#### Activity stream:

- Follow an account.
- List blogs you follow.
- List accounts you follow.
- List account followers.
- Render an activity stream based on the blogs you follow.
- Render an activity stream based on the accounts you follow.
- Share a post with your followers (the post will be included in their activity stream).

#### What to expect?

Users will be able to deploy a Substrate node and web UI that includes our modules. This will allow a user to send an extrinsic that let's them to upvote or downvote a post or a comment. After a user voted on a post or a comment, a rating of post or comment should be updated respectively. A blog rating shoud be updated when a rating of its posts updated. An account/member reputation should be updated when a rating of their posts or comments updated. Ratings and reputation will be stored and updated in Substrate storage in related structures (blog, post, comment, account) and should be visible somewhere on web UI.

A user should be able to follow another account or blog by sending an extrinsic. It should be possible to see all followers of an account or a blog, and accounts or blogs that an account is following. A user should be able to unfollow any blog or another account that they are following by sending an extrinsic.

A user should have an activity stream on web UI that contains posts from blogs or by accounts that a current user follows. Also a user should be able to share an interesting post with their followers by sending an extrinsic. All shared posts will be included in acivity streams of user's followers.

#### Documentation & Docker:

Both documentation and Docker containers should be updated to reflect new features and changes introduced in this milestone.

### Milestone 3 – SEO, Full-text search – 1 month – $10,000

#### SEO optimizations:

It’s essential for any blogging platform or a social network to be indexed by the search engines so other people could find your blogs or posts through a web search.

- Integration with Next.js for server-side rendering of read-only parts: view blog, post, comment, and public user’s profile.
- Server-side rendering of a blog.
- Server-side rendering of a post.
- Server-side rendering of every comment.
- Server-side rendering of a user profile. (Profiles should be optional)

#### Full-text search:

Currently, it’s hard to build a full-text search service in a decentralized way because we don’t have a proper incentivization model for technology that is not built on blockchain (as a full-text search is). That's why we will implement it as a centralized service built on the open-source technology: [ElasticSearch](https://www.elastic.co/).

- Full-text search for blogs.
- Full-text search for posts.

#### What to expect?

Users will be able to deploy a Substrate node and web UI that includes our modules. This will allow a user to send an extrinsic that let's them create a new blog, post or comment or edit any of this entities. A web UI should support a server-side rendering of any blog, post or comment. This means that HTML content of a page that contains a blog or post should be rendered on a backend before sending this page to a user. This could be checked by looking at the source of the page in a any web browser.

Text content of every blog and post should be indexed by ElasticSearch DB. This means that a user should be able to search for blog or post they are interested in by typing in a search input on the top of web UI. After "Search" button clicked, a user will see the search results (blogs, post) related to their search phrase.

#### Documentation & Docker:

Both documentation and Docker containers should be updated to reflect new features and changes introduced in this milestone.

## Additional Information

### What work has been done so far?

Here is a list of things that have been implemented so far on both Substrate runtime and UI sides:

- Create a new blog.
- Edit my blog.
- List all blogs
- Create a new post on a blog.
- Edit my post.
- List all posts in a blog
- Add a new comment to a post.
- Reply to a parent comment.
- Edit my comment.
- Render a tree of comments below a post.
- Upvote/downvote a post.
- Upvote/downvote a comment.
- Follow/unfollow a blog.
- List blog followers

Below you can see the demos of working functionality (click on an image to watch on YouTube):

#### Demo: Web UI

[![Subsocial demo: Web UI](http://i3.ytimg.com/vi/dmz7cEjj1Eg/maxresdefault.jpg)](https://www.youtube.com/watch?v=dmz7cEjj1Eg)

#### Demo: SRML part 1: Structs and storage

[![Subsocial demo: SRML part 1: Structs and storage](http://i3.ytimg.com/vi/TRcp1QdLSrU/maxresdefault.jpg)](https://www.youtube.com/watch?v=TRcp1QdLSrU)

#### Demo: SRML part 2: Events and extrinsics

[![Subsocial demo: SRML part 2: Events and extrinsics](http://i3.ytimg.com/vi/ILDWLPUd0vs/maxresdefault.jpg)](https://www.youtube.com/watch?v=ILDWLPUd0vs)

### Are there any teams who have already contributed (financially) to the project?

No.

### Have you applied for other grants so far?

No.

### Are there any other projects similar to yours?

If you compare the things we are working on now at Subsocial, Steemit could be considered as the most similar project.

### How is your project different?

We are building our project on Substrate and because of this we already have quite different architecture. Moreover, we have our own vision of the software for decentralized social networks.
