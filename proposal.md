# Social Network Simulator

This is a proposal for _Culture_, a social network simulator designed and developed to teach students about bot development.

## Overview

_Culture_ will be an agent-based simulation of a simple social network modeled off of Twitter. As such, the simulation will consist of the following (each part is elaborated further below):

- users communicate in a rudimentary _language_
- users have different _personalities_
- each user will have a _feed_ of messages from people they follow and include promoted/ad messages
    - here students can potentially design their own news feed algorithms and see how that affects individual/public opinion
- users can _message_, post _media_, block, be blocked, be banned, follow, unfollow
- messages and media _influence_ users
- the network responds to and affects outside _events_

## Motivation

So much of our exposure to and understanding of the world beyond our immediate experience is mediated by social networks, which is to say by newsfeed algorithms and other individual users of these networks. Students should develop a stronger literacy in these dynamics if they are to adequately navigate this information ecology.

This literacy is best developed by direct interaction with these social networks, such as Twitter or Facebook, rather than through theory alone. However, working directly with these networks may be impractical in that they are massive, closed-source, and limited in access. For instance, due to API limits it is impossible to survey or conduct analyses of the entire population of the network, or to examine in detail its inner operations.

Furthermore, there is no room for counterfactual speculation in these existing social networks. For example, we can't intervene and change the behaviors of all users and see how information propagation changes as a result. This limits the pedagogical value of working directly with, for example, Twitter or Facebook.

A simulated social network addresses these concerns. It can be designed to model the dynamics of its real counterparts, it can be entirely open in that students have access to all the network's data, and its parameters can be tweaked to see how information propagation evolves under different circumstances. Students can develop bots on this network without worrying about API limits, spam protection, and so on. In contrast to the black-box nature of a real social network, a simulated social network functions more like a sandbox.

## Agents

The simulated agents are individual users of the social network. They are randomly generated to have particular personalities and interests (see below). Their generation is part of the simulation's initialization. Students do not directly interact with these agents, but can indirectly interact with them via, for example, ads and bots they create (see below).

## Language

Dealing with natural language is difficult even for experienced developers and advanced researchers in the topic. Broadly, the problem of natural language in the context of bots can described in two parts: _understanding_ and _generation_. Both are very difficult and beyond the scope of the courses that this simulation is designed for, which includes introductory classes.

To avoid dealing with natural language, the simulation will consist of a very basic grammar and a relatively small vocabulary which can be easily expanded as needed. Because of its relatively simplicity, the same natural language processing techniques that are currently used for "real" languages can also be applied, but with greater success, and better yet, simpler heuristics will go a longer way. Thus students will not need to have a deep understanding of, for example, word vectors or TF-IDF, but may develop their own simpler techniques that will still be effective.

This simpler language will consist of verbs, nouns, and modifiers (adjectives and adverbs) (collectively, "terms"). Because the courses are assumed to be taught in English, this language will be reflective of English.

These terms are combined into formal propositional statements, e.g. `single-payer-healthcare + country -> < freedom`, which expresses the opinion that implementing single payer health care in this country will cause (`->`) a loss (`<`) of freedom. (This is just a sketch of the syntax; it's subject to change).

This is a bit limiting; there is no room for poetics, for instance, but will provide a strong starting point that can be expanded on later.

The design of this language will involve developing a network of terms (i.e. defining term associations), such that terms represent mixtures of other terms and values in the simulation (e.g. individuality/collectivism, see "Personalities" below). This term association network is opaque to the students; they do not get to see what these terms mean to the agents in the simulation. As with the real world, they must use algorithms or their own intuition from observing the network to determine what language best communicates their messages.

For example: the term "car" may be connected to the terms "individuality" and "freedom" to establish that the term "car" symbolically evokes these two ideas. We could then imagine ads for "cars" appeal more to agents with personalities that align more with those concepts relative to agents who, for example, align more with "collectivity" and "freedom".

Terms also have sentiment valences, e.g. "bad" may have a valence of -0.5 to express a negative opinion, whereas "terrible" may have a stronger valence of -0.8, and so on.

Ideally, this term association network is not objective but rather subjective; i.e. differs depending on the particular agent. For example, the term "freedom" may be associated with different values for one agent than for another. However, it is likely that this will be computationally infeasible (though some kind of heuristics could be developed to simplify it).

This term association network also changes over time as terms are used in slightly different contexts. This provides a way for the meaning of terms to change or be entirely inverted, e.g. a negative term being co-opted as a positive identifying term for a group.

The language is the part of the simulation that will require most care in designing - it needs to represent important aspects of how language is used in social networks (e.g. to express opinion/judgement, to harass/abuse, to make propositional statements, etc).

## Personalities

Simulated agents will have could loosely be described as "personalities"; that is, a set of parameters that determines how the agent interacts with others (e.g. aggressiveness/friendliness, within-bubble/outside-bubble, etc) and what their values are (e.g. conservative/progressive, individualist/collectivist, etc). These personalities will be generated randomly, via a Bayes Net (or some similar probabilistic model) that will be editable in some way. A model like a Bayes Net lets us describe assumed relationships between values (e.g. more collectivist agents are more likely to be friendly).

These personalities also determine who agents tend to interact with (under principles of homophily, i.e. like attracts like) and also what kind of messaging resonates with them (e.g. messages about rugged individuality will resonate more with individualist agents).

## Messages

"Messages" are the equivalent of Twitter's tweets. Agents compose their own messages based on their personalities and who they are interacting with. Messages may affect an agent's mood and also their personality (see below).

## Media

Text is not the only important part of a social network - memes and other media (news stories, videos, etc) form a crucial part of their information flow.

## States

Agents' states include their personalities, in addition to other attributes like mood and use frequency (how often they visit the social network) and post frequency (how often they post messages). Mood may affect, for example, how agents interact with other agents (e.g. with more or less hostility). This can be used to model emotion contagion.

## Influence

Based on who they interact with and what other messaging they are exposed to (e.g. targeted ads), the personalities (traits/opinions) of an agent may shift over time. Various social phenomena, e.g. bipolarization, can be modeled here.

## Events

Social networks are not closed systems; they do not exist in isolation. The "outside" world affects what goes on in network, just as what goes in the network can spill out and effect the outside world.

Part of the simulation will support external events (also simulated) that affect and can be affected by the social network, such as an election. The outside event(s) affect what are _popular_ topics (i.e. topics that are _relevant_ and agents are more likely to talk about and respond to) and they can be defined to have some relationship to the shape of discourse in the network.

## Social Network

In this section, "social network" is used not to refer to the platform itself, but to the actual network of relationships between users (expressed by "following" relationships). Some users may be highly connected (many followers), and students may, for example, as part of their strategy (whether for ads or opinion influence) try to target these opinion leaders.

## Visualization

It will likely be too computationally taxing to display _all_ activity on the social network, but students will have access to various views that provide summaries (i.e. mean sentiment towards some topic, number of users talking about a topic, etc). Ideally an API can be provided like a real social network, so that students can build their own visualizations as part of their bot development process, but this may be limited by the size of the simulation.

## Bot API

A simple API will be provided for students to develop their own bots that interact with this network. These bots can follow, be followed, message, etc like agents can and will be the primary way students interact with the social network.

What distinguishes bots from simulated agents is that bots are designed and controlled by students, whereas the simulated agents represent "real" users of the network.

## Learning Objectives

The network functions as a simplified social landscape for students to understand how ads, bots, and news feed algorithms affect opinion, trends, and discussion on a social network, and how that links up with broader spheres of discourse outside of the network. Some students may, for example, design bots that influence opinion in a certain direction, while others may design bots to influence opinion in a different direction, while still others may design bots that root out these interfering bots. Depending on how the network is designed, some students can be the managers of the social network platform.

The goal is for students to develop a comprehensive mental model about the dynamics of social media and communication in the internet age, to peek "behind the curtain" and develop a critical perspective when using social media and reading the news (i.e. develop social media literacy).

## Extensions

In theory this simulated social network can be extended with features that could be present on any social network, such as anonymous accounts, different kinds of blocking and muting functionality, and so on. Thus it can also be a place where students can experiment with new features to see how that affects dynamics on the network.

## Variants

Ideally the simulator accommodates students who are comfortable with programming and those who aren't.

For students who aren't, bot templates could be provided which require little to no programming experience, or another layer can be developed where they "purchase" different bot, marketing, and so on services that run automatically.