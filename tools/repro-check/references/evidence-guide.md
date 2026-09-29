# Evidence guide: where proof lives in a reproduction package

## Environment

Where it lives: In an eval package, check the repro report's environment record and compare it with the issue context. In live mode, check the environment section of the student's draft and the issue/repo documentation.

What good looks like: The report names the OS and relevant tool version. The environment matches what the issue targets, or any important difference is clearly stated.

## Steps

Where it lives: In an eval package, check the reproduction steps in the repro report. In live mode, check the steps in the student's draft and compare required setup with the repository documentation.

What good looks like: A stranger can start from the stated environment, follow the commands/actions in order, and reach the trigger without having to guess missing setup or actions.

## Behavior shown

Where it lives: Check the repro report's output excerpts, logs, screenshots, or other artifacts and compare them directly with the behavior described in the issue.

What good looks like: The evidence demonstrates the specific behavior described by the issue. Evidence of a different or adjacent problem does not count. A cannot-reproduce result is valid when the attempted reproduction and resulting behavior are clearly evidenced.

## Honesty

Where it lives: Compare the repro report's stated outcome with its steps, output, logs, screenshots, and other artifacts.

What good looks like: The report claims only what its evidence supports. A supported reproduction or supported cannot-reproduce is acceptable; claiming success or failure beyond the evidence is not.

## Comms

Where it lives: Check the claim comment and repro comment against the issue context, repo-facts, contribution documentation, comment templates, and any stated AI-use or disclosure policy.

What good looks like: The claim identifies the specific issue and honestly states the planned investigation without claiming work that has not happened. The repro comment describes the observed result specifically. If the repository requires disclosure of AI use, the comments must contain that disclosure and include every detail the policy requires, such as the AI tool used and the extent of its assistance. Missing a required disclosure fails the repository-conventions check.
