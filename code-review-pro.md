So I'm watching [this course made by Curtis Einsmann](https://app.gumroad.com/d/96a466204a34554ae86ea025ca48985d) and it's being great.
It helps to structure the values, goals and approaches related to the code review process.
And this file isn't a conspect of the course, but is heavily inspired by the course.

### emotionally uncomfortable things
+ my PR was assigned to some people, not my teammates, and they don't seem to look into it. Especially if that people are some lead engineers, and that PR is a small "infra" one, like a Podfile change, or a Codeowners file change.<br>
  **solution**: wait for 24 hours, then ping them in Slack without a hesitation. as a code review is blocker, there should be some balance btw the speed of it, and the fact that the reviewers also have some high prio stuff to handle
+ someone asks me to change a Swift line with `extension` to a `private extension`, and I know I should have checked that by myself, but feel irritated as it's more about the style, than about the clean code / compiler optimization, and I always forget to check that. The same stuff for a `final class` vs `class`.<br>
  **solution**: either push that to be added to a linter, or create a local linter helper. The hardest part of it is of course the context: should that extension really be a `private` one?
+ I don't like some change, but can't decide if it's a blocker<br>
  **solution**: TODO
