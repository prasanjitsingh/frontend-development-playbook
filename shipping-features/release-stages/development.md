# Development

This stage is pretty self explanatory and isn't really part of the release stages. This is where the hard work happens to bring the feature in to existence. However, this stage does deserve mentioning as a feature may well end up back here if you need to make changes based on feedback from one of the other stages.

## What to focus on in this stage

The obvious answer is developing the feature. However there is another side to this. You really want to ensure that your understanding of the problem and the solution you're building is the same as the people that experience the problem in the first place. It's no use building a feature for a problem, if you've not understood the problem correctly in the first place.

This stage also allows for clarification of changes to the feature scope based on learnings that have occurred since development began.

Therefore, it's super important, while developing, to ensure that you get someone that has some stake in the feature to sanity check the solution before merging it to ensure it fixes the problem in the way they expect and that everyone is on the same page. 

The way to do this? Lightning preview links!

During development, you have the ability to send preview links of your in progress PR to people to test and verify. Make the most of this as it's a super valuable tool that allows you to get that extra confidence that what you're shipping is high quality.

## Who to engage in this stage

Most of the interactions in this stage are going to be with the Support team, so your first port of call should be Gary McGrath. Discuss with Gary the feature you'd like tested and how many people you might want to look at it. If Gary doesn't already have it, send him a lightning preview link which he can share with the selected support users.

You may also want to get some feedback from stakeholders or customer/marketing focussed people. You can always share a lightning preview link with James Doman-Pipe and Alicia Carney who will have a good idea if the feature is headed in the direction that they know users are expecting.

If this is a feature that will require some self service documentation created, now is also a good time to send Kelly O'Brien a link so she can start to become familiar with how the feature will function. She will also be able to give you some valuable feedback on any glaring issues with the UX from a user's perspective.

## A note on lightning preview links

Development is really the only time we should be using lightning preview links. Once a feature has been merged in to the `master` branch, it should be accessed via feature flags and therefore our external users shouldn't really be exposed to lightning  
preview links.

Obviously, there is always an exception to a rule and there may well be circumstances where it is desirable to share a lightning preview link with an external user. But we lean towards not sharing them to anyone outside the company when possible.

