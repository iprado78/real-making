 spitballing after two drinks at the bar, I think we can expect the next century to be characterized by the long recoil of 19th Century industrialization and colonization.  We'll continue to see a lot of catchup growth in developing areas, especially China, India, and Africa.  We'll also see continued economic stagnation in the West (unless there's a lot more immigration). The x-factor is dealing with the accelerating human dislocation and resource waste of climate change.
 
 [Code smells](https://refactoring.guru/refactoring/smells) are a good example. If I am imperatively updating two pieces of related application state in a method call, that's a sign something has gone wrong, even if I don't know what.  Receptivity here means staying with the smell and getting curious about its source.  Likely, there's coupling in my state that a better way of modeling it, with declaratively specified dependencies, would reduce.  I should update one thing from the method call and let the class internals reactively trigger an update to the related thing.

Another area in which receptive task engagement is useful is in dealing with 

In that context, it's the name for the spiritually realized state, which, in typical Buddhist fashion, has lots of synonyms in Dzogchen that provide slightly different methodological indications for practice ("Great Perfection", "self-liberation", "primordial awareness", etc.).

Say you, dear reader, are developing a user-facing web application.  The app lets you set up a watchlist to track price changes of some prized resource, such as early editions of the [Futurist Manifesto](http://bactra.org/T4PM/futurist-manifesto.html) on [Ebay](https://www.ebay.com/itm/362090934742?hash=item544e4d31d6:g:t5gAAOSw0xRZnXD~).  Users manage a queue of notifications that are sent when an edition becomes available on the market in their configured price range.  Your job, this development iteration, is to implement a button displayed inside in these notifications that allows a user to make a bid at the listed price.

First, you send Amazon license fees for adapting their [heroic innovation](https://en.wikipedia.org/wiki/1-Click), the one-click transaction.  It was downloaded by some late 90s business process guru straight from the mind of God, and they deserve to get paid in perpetuity.  Legal niceties out of the way, you implement a button interaction with two possible result states in the UI:

1a. The notification disappears
2a. The user sees a rather honest inline message from the system, "Sorry, too slow, either on the side of you're trigger finger, my latency, or the unavaoidable chaos of packet hops".

These two UI states map to the states of the underlying transction:

1b. Bid success 
2b. Bid failure

For simplicitly, let's assume bids are immediately accepted or rejected by a matching engine, rather than entering into some extended auction.

Then, you receive another requirement from your product manager.  The user should see a confirmation message on success.  Notifications shouldn't just disappear, she says, because that's jarring and confusing. (You, a rationalist engineer, would say "cleaner" rather than "jarring and confusing", but many users do need these mysterious, all-too-human crutches).  Finally, the product manager thinks both the confirmation and error messages should normally fade out after 3 to 5 seconds, though there's an affordance for them to preemptively go away if the user acknowledges them with a click.  When the confirmation message goes away, the underlying notification is dequeued from the displayed list.  When the error message goes away, the notification is back in its initial state, ready for another one-click bid. 

Now you, the developper, are able to achieve a state of flow.  The problem is a bit more interesting.  You're going to have to set up and orchestrate races between the message timers and message acknowledgements (i.e., clicks).  You smile because you know you can leverage your knowledge of Reactive programming constructs:

```

Map transaction completions to  -> 
  Pipe of ->
    Concatenatation of ->
      Entry to post-transaction message state ->
      Map race between timer and acknowledgement click to -> 
      Exit from post-transaction message state

      What characterizes this as a flow state is your experience of expressing practical mastery over the affordances made available by your current problem situation.  That mastery comes from pattern recognition.  You recognize the problem situation as an instance of a general type you have run into before.  You have a canonical, or at least robust, solution to the problem available in nearby cognitive space. 


      For example, in our _Futurisme_ market app,  you need to do something in addition to setting up the race between the timer and click that advances the message state.  You're going to have to model a UI state--the state of awaiting for the timer or acknowledgement--that's independent of the state of the underlying transaction.  The state of the transaction remains constant while the UI enters and exits the post-transaction message state.  You're first thought is

> Ok, I'll extend the interface of an Offer (the object of a bid) to create a UIOffer, which will model any UI-only state or properties.

Those UI states are:

Pending (Waiting for bid, Returned to on exit of Error) ->
Error (Error message state entered on fail of bid) ->
Confirmed (Confirmed message state entered on success of bid)Completed (Confirmed message state exited) >

This might work, but it smells in several different ways



 In a trad Dzogchen context, the practice path begins with a Dzogchen master directly indicating the realized state to their student, usually through some means of esoteric transmission (gesture or speech, ritualized or informal).  Student practice and teacher instruction then co-evolve around finding the means for the student to abide in the realized state.

I know this merely second hand, through reading books like [The Crystal and the Way of Light](https://www.shambhala.com/snowlion_articles/the-crystal-and-the-way-of-light/).  My history of Dzogchen practice begins and ends with Evolving Ground, and our initiation into practice is not trad. To start with, teaching authority is embodied in a [Spiritual Friend](https://en.wikipedia.org/wiki/Kaly%C4%81%E1%B9%87a-mittat%C4%81) model, rather than a Guru model. The difference can be seen esoteric.  Charlie's teaching, as evidenced in the Stoa episodes, explicates Vajrayana view and method at the level of principle and function. In the absence of esoteric transmission, there are concomittantly different signals for the presence of spiritual authority.  Authority is expressed in a Spiritual Friend through

1. Experience embodily expressed competence that drives one's own understanding

rather than 

2. Ritually ordained and vouchsafed lineage. 

In a trad context, (2) is meant to track (1) (at least in the tradition's idealization).  In explicitly abandoning (2), a spiritual group opens up to a sligtly more fluid, context-bound conception of spiritual authority.  In some contexts, a student with less experience and no formal teaching role may spontaneously manifest the best teaching insight to others.  To tie this back to the point about non-esotericism, that can happen because understanding at something at the level of "principle and function" isn't magic.  You may need [100,000 reps](https://studybuddhism.com/en/advanced-studies/vajrayana/tantra-theory/overview-of-tantra/tantra-ngondro-empowerments-and-ritual-practice) to get to get to the base of Tantra, or [you may not](https://aroencyclopaedia.org/shared/text/n/ngondro_ar_01_ncr_eng.php).  The same would apply to Dzogchen and esoteric initiation.

That said, the relative horizontality of spiritual authority shouldn't be mythologized or overstressed.  Mythologizing can obscure where the real lines of authority are concentrated in a spiritual group.  Overstress can lead to a delusion of specialness in new practioners.  Whatever else spirituality is, it's manifest through an embodied set of skills.  Like any set of skills, the most reliable path to acquiring them is some combination of natural talent or affinity, mentoring, and diligent "practice" in the ordinary Malcom Gladwell sense.  This is true even if formal practice comprises the "no-technique" methods common in non-gradual spiritual paths, such as Dzogchen.

Which brings me back to what I mean by "congruent" for the purposes of this newsletter.  Non-gradual spiritual paths usually go along with "non-dual" views. In a Dzogchen context, non-dualism includes the doctrine that the realized state and ordinary awareness are not fundamentally distinct.  They are also not merely identical.  Those statements can't be unpacked rationally, so non-dual thinkers usually really on poetic metaphor, like the one about [mountains and rivers](https://www.goodreads.com/quotes/9085645-before-one-studies-zen-mountains-are-mountains-and-waters-are).

Phenomenologically, what grounds non-dual doctrine are experiences or intimations of spiritual realization sparkling through ordinary awareness. The finding of those sparks can be experienced as a sense of maximal fit with one's situation and environment.  They have an aspect of the world feeling fundamentally okay, right here, right now (even when it is obviously not in any ordinary, mundane sense).  I am calling that "congruence".

The newsletter is dedicated to elucidating congruence in specifically displays of practical knowledge and wordly activity. I highlighted three kinds of practical knowledge in the introduction: (1) programming computers to do things effectively , (2) teaching or managing others's to be able to do things more effecitvely, and (3) embodied ability to do things effectively


That's a bit rich for what I want to talk about in a lot of instances, though.  I'd start with common description of a flow state.  As it relates to individual activity, "flow state" usually implies a kind of tunnel vision.  Your skills and problem situation combine to produce a situtation 

 that includes kindness, recognition, and receptivity to what's going outside of your tunnel of awaress.  That's a bit thin as a definition.  I hope to put body on it with concrete examples.



If "artificially suppressed" is referring to central bank stuff, I'm probably starting from very different baseline assumptions. I don't think economies have "natural" rates of volatility or growth that exist in independence of fiscal and monetary policy or legal frameworks.  It's a stack of "artificial" interventions all the way down, starting with how entitlements to property get legally established. The full stack produces complex, dynamic incentive structures that in turn generate economic behavior. Some of that behavior exhibits aggregate trends economists can study, but it's very noisy.  If, however, over long enough time horizon, you see a consistent trend-line, then that's the natural volatility, not what some theoretical model in abstraction from real-world interventions would tell you.

I believe there are social minorities situated in power structures that disadvantage them.

I believe we have an obligation to think through every lever of institutional change that can and should, _and can't and shoudn't_, remedy that. Your state fair doesn't need to make amends for Native genocide.

I think the categories we use to pick out minorities disadvantaged by power arrangements are necessarily problematic, because they don't track stable groupings in nature.

I think the impetus to think there's real universal human experience underlying being in an artificial grouping is a constant temptation, but I think the attempt temptation is problematic, because the groups aren't real things in any robust sense, so there can be a coercive logic to making universal claims on their behalf.

But of course being classified a certain way, and self-classifying a certain way, does real things to people. In the aggregate, those real things may generalize.  And denying those generalizations can be, to use the wornout phrase, "gaslighting".  We have 500 years of history to prove it. It's a complex thicket. If I have a distinctive view, it's that the various "isms" should be thought of as targets of explanation, rather than explanatory. "Patriarchy" doesn't explain why I do things; it's a name that summarizes a complex set of factors for why I do things, for what they amount to.  Those factors may be very different in different contexts, so "patriarchy" will name different things.  There's no grand pyramid of oppression that starts with microaggressions and ends in genocide. 

_Pseudo-Isaac Chotiner: yet you seem to mostly be talking about/to white dudes__

The balance of the references, and I can judge of who my initial 

Q: Can you elaborate on the reference to "Satanic Mills"?

Q: Some would posit World War I as a matter of primarily elite-driven conflict. How would you square (or refute) that with respect to the idea of elites retreating from worldly business?

Q: Say more about the ethos of rejecting appeals to tradition?

Q: What is "upskilling desire?"

Q: What do you mean by "real-making"?

Q: Who are these pleasant bureaucrats and sexy murder poets?

Q: My intuition is that religions that impose disciplines of living deeply touch the self. You cannot live as an observant practitioner without it changing you. Intersect that with your discussion of leaving selves complacently untouched.

Q: Speak more about the invisible others who exist by courtesy of pretense.

Q: "There is no purpose" vs. "There is no ONE purpose". Two different versions. Same/different?

Q: Explain your terms, "virtualizing", and "virtualist".

Q: "our extractive way of relating to real, non-virtual others." Pretty harsh. I'm sure many would disagree, but sense that this could be clarified so that many agree. How would you do so?

Q: My personal experience does not jibe with the East-to-West starter kit (none of the books, no psychedelics, no secular meditation group, etc.). How common do you think the pattern you refer to is among your demographic, or altogether these days?

Q: I've never heard of Ernst Cassirer. Can you give me a short primer of what you view as most salient in his works?