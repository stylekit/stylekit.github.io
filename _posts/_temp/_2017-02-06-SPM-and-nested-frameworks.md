My notes on SPM + XCode + Nested frameworks<!--more--> 

## Pretext

You want to develop an awesome app: Like a Hackernews reader app. You have a time budget of a weekend. Which forces you to priorities ruthlessly. You want to make some innovative GUI that stands out. Lots of nice animation via gestures etc. You need 3 frameworks to do it: Element for GUI awesomeness, AlamoFire for simple communication with hackernews.com. SwiftyJSON for parsing data from AlamoFire. Now you want to download these dependencies and build them in a way that a single person can work on it and a team. So you need your code to be on github. 

The chain of dependencies looks like this: Its only 2 level deep. But can go deeper if needed. 
``[HackerNewsApp] -> [AlamoFire, SwiftyJSON, Element -> [swift-utils]]``

