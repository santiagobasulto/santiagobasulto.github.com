---
layout: post
title: "How we built an MVP in 15 days"
category: git
tags: programacion git alias shortcut
published: false
---

This is the story of how we developed our MVP in less than a week without writing a single line of code. **Important: These experiments are currently undergoing and things can change. Stay tuned.**

Some time ago we had an idea: Education needed to be improved. It was a bold idea... _"One does not simply change education"_. That's why we were both excited and scared at the same time. We decided that we wanted to do things differently... Validate quickly and get users from day one.


You can read about why we decided to create rmotr.com in more detail in [this other post](). I'll just summarize our first hypothesis:

* Hipothesys 1: To learn how to code it's fundamentally important to interact with other people. Learning how to code is not about learning the syntax of a programming language, but also how to interact, how to get help, how to loose the fear to break things, etc...

* Hipothesys 2: Online courses are great because they lower the entrance barrier. They're cheaper than college/physical bootcamps, you can take it from anywhere in the world, you only need a laptop, and there's flexibility regarding times. **But they're fundamentally flawed because they don't provide human interaction**

* Hypothesis 3: Remote work is here to stay. It's technologically viable. More and more companies are doing remote work and it's actually working. We can take that to education.

From those two hypothesis we derivated the our main one: **rmotr.com would create remote courses that would have the best of the physical and the online world and it'll be a great learning experience for our students** We decided to create two courses: one really basic to teach people how to program and other one more advanced to teach Python in depth (programming experience was required). This way we could test our hypothesis with different sets of users with really different needs.

Now, if we'd have this very same idea 1 year before we'd have started writing code to create the next big remote-learning platform, setting aside the most important facts to validate. That's why we promised ourselves to avoid writing code. This is what we did...

## The MVP

The first thing we needed to tackle was the actual class. How to create a class where everyone could be part of at the same time? The obvious answer was to use Google Hangouts. It's an amazing and robust tool. At my job we've used it for daily scrum meetings for more than a year and it feels a lot like being in the same room.

We also needed an online/collaborative IDE to allow people to work together. The clear winner in this battle was cloud9. It's a great tool. Even though it has some bugs the awesomness it provides exceeds any grief that those bugs can introduce. Plus, using cloud9 we could avoid all the initial setup
 which usually is the number one reason that lowers students' morale.

Finally we also chose to use Google Drive to share files and a G+ community to drive conversation inside each course.

## First experiments

We needed a set of students to be part of our first experiment. We went to the right place to look for them: learnprogramming subreddit ([/r/learnprogramming]()). We [created a post]() sharing our feelings and telling everybody what we were trying to do. **People went bananas!** We've got more than 500 sign ups of people trying to get into the first course. When we started this we just needed 5/6 students per class. We didn't know what to do with that many people!!. We knew one thing: **People don't take free stuff seriously**. So we had one clear goal: We wanted to be really sure that people joining the course would be committed to it. We thought that people dropping out could demote the quality of the course and screw up our experiment. So we decided to put a really high barrier to accept people. We asked a bunch of (stupid and maybe nonsense) questions and made them complete a simple programming puzzle. Of course we knew that some people couldn't even code, but we wanted them to at least send a file with a comment saying _I don't know how to solve this thing_.

Less than half of people that had originally signed up did the whole thing (questions + puzzle). That was a relieve, we guessed correctly. If someone couldn't even take the time to answer some questions, he/she would not have completed the course by any chance. We still had more than 200 students to select, so we just went one assigment at a time and did a finer selection. We were really hard with ourselves though: we decided to take the experiment to the limit. We selected people from different countries, different timezones and cultures. We knew that it'd make things harder, but it was worth trying it. We had people from the US, Australia, Latin America, Canada, Russia, Romania and the UK. We also were selected young and "old" people, working guys, college students and high school students.

We got a small subset with about 100 students and we decided to do Hangouts with them. We organized them in batches with 10 students each and set calendar events with all of them. Many didn't show up, which made our job even easier. From the remaining subset that showed up and were in shape to be selected we just picked them up randomly (yes, with a Python script).

## The ball started rolling

We had the "educational" part covered. Our experience in the local university was really helpful. But we still had a bunch of things to figure out. It was kind of a mistery how the first classes would turn out, we didn't know what to expect. We decided to use a really practical methodology. We'd teach the students some topic in no more than 15/20 minutes and we'd give them a bunch of assignments to do in groups; lecture and coding, lecture and coding. The groups were selected randomly each class; that way we were sure everybody got to work with everybody in the class. **Group work turned out to be awesome** The students were really happy getting their feet wet with code from class 1. Having cloud9 previously configured was really helpful because they didn't have to stop not even 1 minute installing stuff. One thing that really impressed us was the fact that they'd help each other explaining things in different ways for students that didn't get it. A student that just got the concept was a better teacher that ourselves. Not because he/she knew more, but because they'd know how to express it to their fellow classmates. That's something that we didn't know and it was a really pleasant surprise.

Each class had homework. We'd randomly create groups and distribute the assigments that they'd have to complete for next class. The idea was that they should find a time to get all online and work on those assigments together. This didn't turn out so well. Really few students had the motivation to push the other guys to get online and work together and it was one of the bigges bummers we had. Most of the time they'd just work on the assigments by themselves and would get online 15 minutes before class to share what the had done. Not really cool in our perspective. Certainly one thing to improve.

## The results of the first batch

After 8 classes the courses were done. We sent a survey where they could tell us how was their experience with the course. We asked them different things like: overall impression, things to improve, problems they had, etc. We also asked if they'd pay for the course now that they knew what it was about. We know that it doesn't provide good validation, but most of the people said they'd pay for the course. We also had final classes where we'd say goodbye and we'd also ask them more stuff related to their experience with the course.

From what we could get we concluded that **the courses were a complete and huge SUCCESS**. All (except 1 student) loved the course. MOST of the people compared it with traditional online courses and all agreed that it was a much faster and efficient way to learn. These are some quotes we got from them:



* Ídea primaria/inicial. La semilla. Demostrar hipótesis.
* Experiencia previa, no quería demorar mucho.
* Evaluar el público/canal correcto para hacer mis experimentos
* Nada de código ni pérdidas de tiempo ni dinero.
* Post en reddit (link al post + screenshots) -> X signups
* Google form + doodle.
* Armado de los cursos:
  * Metodología
  * Hipótesis
