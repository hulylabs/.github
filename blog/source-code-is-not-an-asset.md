# Source code is not an asset -- it's posion

Many people think that source code is an asset. It's not. I'm not new with such an idea here, and you can find a bunch of articles on the internet that say that source code is not an asset -- it's liability. But I want to go a bit further and say that source code is not just not an asset -- it's poison.

Funny thing that many people and teams, deep inside understands that at very intuitive level, but never raise this issue or even discuss. And shared (wrong) understanding of source code as an asset prevails. This is a big problem.

Let's start with the definition of an asset. According to [Investopedia](https://www.investopedia.com/terms/a/asset.asp), an asset is a resource with economic value that an individual, corporation, or country owns or controls with the expectation that it will provide a future benefit.

First source code is obviously a "resource". So what's the economic value of source code? It's the value of the software that can be built from it. But the software is not the source code. The software is the product that can be used to solve some problems or provide some value. The source code is just a way to build the software.

Another wrong and common misunderstanding is that to build more features, or faster, or better (whatever it means) software you need _more_ source code. There is very wrong thing which is in heads of engineers, managers and business owners: more code equals more features. This is _completely_ wrong. More code means just more code and nothing else. Let me give you very chlidish example demonstrating this fact. I can write 3 lines of code adding three "features" and after I will write one line adding much more features including those three:

```typescript
const feature1_add5(x: number) => x + 5
const feature2_add10(x: number) => x + 10
const feature3_add25(x: number) => x + 25
```

or we can do it like this:

```typescript
const better_add(x: number, y: number) => x + y
```

You can say this is stupid example, and of course everyone will do the latter, but you're wrong. Almost every large codebase uses first approach. I have never seen a codebase where 50%-90% of the source code could not be discarded, destroyed, and replaced with a small fraction of lines. This include major open source projects, Fortune 500 companies, and various startups. And this happens for many differnt reasons.

Why more source code is bad? Because source code is what kills you, what kills project, product, and company. Complexity only growing up and you need to develop it further, you need to maintain it, and you need more and more people to do that. And more people means more communication, more coordination, more bugs, more problems. And more problems means more time to solve them, more money to pay for that time, more stress, more frustration, more burnout.

Eventually any codebase dies because of it's source code. Some companies start call it "legacy code" and try to rewrite it from scratch. This is quite often scenario. Some companies doing this every 3-5 years. And they never learn. They never learn that source code is not an asset -- it's poison. It's poison that may kill company, project, product. And they after "legacy" codebase thrown out start to produce new posion very enthusiastically. Funny part that faster they produce it, faster they die.

Of course there are exceptions. There are very few people who understand that. You can say, OK, Linux Kernel. This is great example. But there is Linus Torvalds, who understands that source code is a posion and work with it as everyone should work with source code. The only way to work with source code is the same as people works with dangerous chemicals.

You need to be very careful, you need to be very responsible, you need to be very professional. Try to contribute to Linux Kernel and you will see how hard it is. Please try to contribute something to Linux Kernel and you will see how fast you will be sent to fuck yourself beacuse you're not careful enough.

OK, that's Linux Kernel, but I'm pretty sure your manager's name is not Linus. Your manager is opposite. I believe she want you to contribute more code, any code, and maybe even will give you achivement and bonus for number of lines you contribute. That's common but very funny. People giving kudos to each other for making things which goes them down and eventually will kill. And they want this to happen as fast as possible.

And more words on poison. Poison is small amounts can work as a great cure. Ancient medicine used posion widely to heal people. Posion is good in small amounts. But when there is a lot of it, it kills. Source code exactly the same. We can't ship products without source code. And in small amounts souce code is awesome. But large amounts of code kills.

OK, let's summarize:

- More code does not mean more features. Actually it's upside down, if you always want to minimise size of codebase you can end up with much more feature implemented in much smaller codebase.
- Source code is not an asset. It's a liability. It's a poison. It's a dangerous chemical. It's a weapon of company desctruction. You should avoid producing it as much as possible. If you can burn some code in your codebase right now, just burn it.
- You should not be thankful to anyone how adds more code to your codebase, but you should be very thankful to anyone who removes code from your codebase. This is the only way to survive.

# Source Code is Not an Asset -- It's Poison

Many people believe that source code is an asset. It is not. I'm not the first to suggest this idea; there are numerous articles on the internet asserting that source code is not an asset -- it's a liability. However, I want to take this a step further and say that source code is not just a liability -- it's poison.

It's funny how many people and teams, deep down, understand this at a very intuitive level but never raise the issue or even discuss it. And yet, the shared (incorrect) notion of source code as an asset prevails. This is a significant problem.

Let's start with the definition of an asset. According to [Investopedia](https://www.investopedia.com/terms/a/asset.asp), an asset is a resource with economic value that an individual, corporation, or country owns or controls with the expectation that it will provide future benefits.

Source code is indeed a **resource**. So, what's the economic value of source code? It lies in the value of the software that can be developed from it. However, the software is not the source code. The software is the product that can be used to solve problems or provide value. The source code is merely a means to create the software.

Another common misunderstanding is that to build more features, faster, or better (whatever that means) software, you need _more_ source code. This is a deeply flawed notion that is prevalent among engineers, managers, and business owners: more code equals more features. This is _completely_ wrong. More code simply means more code and nothing else. Let me illustrate this point with a very simplistic example. I could write three lines of code adding three "features", and then I could write one line adding many more features, including those three:

```typescript
const feature1_add5(x: number) => x + 5;
const feature2_add10(x: number) => x + 10;
const feature3_add25(x: number) => x + 25;
```

Or we could do it like this:

```typescript
const better_add(x: number, y: number) => x + y;
```

You might think this is a silly example, and of course, everyone would choose the latter, but you're wrong. Almost every large codebase uses the first approach. I have never seen a codebase where 50%-90% of the source code could not be discarded, destroyed, and replaced with a small fraction of lines. This includes prominent open-source projects, Fortune 500 companies, and various startups, and it happens for many different reasons.

Why is more source code bad? Because source code is what ultimately kills you, kills projects, products, and companies. Complexity only increases, and you need to continue developing it, you need to maintain it, and you need more and more people to do that. More people means more communication, more coordination, more bugs, more problems. And more problems mean more time to solve them, more money to pay for that time, more stress, more frustration, more burnout.

Eventually, any codebase dies because of its source code. Some companies start calling it "legacy code" and attempt to rewrite it from scratch. This is a quite common scenario. Some companies do this every 3-5 years. And they never learn. They never learn that source code is not an asset -- it's poison. It's a poison that may kill a company, project, product. And then, after tossing out the "legacy" codebase, they start producing new poison very enthusiastically. It's ironic that the faster they produce it, the faster they meet their demise.

Of course, there are exceptions. There are very few people who understand this. Take the Linux Kernel as an example. This is a great example. But there is Linus Torvalds, who understands that source code is poison and works with it as everyone should. The only way to work with source code is the same way people work with dangerous chemicals.

You need to be very careful, very responsible, and very professional. Try to contribute to the Linux Kernel, and you will see how challenging it is. Attempt to contribute something, and you will quickly realize how sternly you will be rejected if you're not careful enough.

OK, that's the Linux Kernel, but I'm pretty sure your manager's name is not Linus. Your manager is the opposite. I believe they want you to contribute more code, any code, and perhaps will even reward you with achievements and bonuses for the number of lines you contribute. That's common, but also very ironic. People giving kudos to each other for making things worse, which ultimately leads to downfall. And they seem to want this to happen as quickly as possible.

And a few more words about poison. In small amounts, poison can serve as a great cure. Ancient medicine widely used poison to heal people. Poison is good in small amounts. But in large amounts, it kills. Source code is exactly the same. We can't ship products without source code. And in small amounts, source code is awesome. But large amounts of code are lethal.

OK, let's summarize:

- More code does not mean more features. In fact, it's the opposite; if you always aim to minimize the size of your codebase, you can end up with many more features implemented in a much smaller codebase.
- Source code is not an asset. It's a liability. It's poison. It's a dangerous chemical. It's a weapon of company destruction. You should avoid producing it as much as possible. If you can eliminate some code from your codebase right now, just do it.
- You should not be thankful to anyone who adds more code to your codebase, but you should be very thankful to anyone who removes code from your codebase. This is the only way to survive.
