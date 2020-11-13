## Scala Library template

This is a template repository with some of the learnings from OSS Scala ecosystem applied.

* **Compile and Publish**

    |                | JVM | Scala.js (1.x) | Scala Native (0.4.0-M2) |
    | -------------- | --- | -------------- | ----------------------- |
    | Scala 2.11.12  | ☠️   | ☠️              | ✅                       |
    | Scala 2.12.12  | ✅   | ✅              | ☠️                       |
    | Scala 2.13.3   | ✅   | ✅              | ☠️                       |
    | Scala 3.0.0-M1 | ✅   | ✅              | ☠️                       |
    | Dotty 0.27     | ✅   | ✅              | ☠️                       |

* **Running tests**

    |                | JVM | Scala.js (1.x) | Scala Native (0.4.0-M2) |
    | -------------- | --- | -------------- | ----------------------- |
    | Scala 2.11.12  | ☠️   | ☠️              | ✅                       |
    | Scala 2.12.12  | ✅   | ✅              | ☠️                       |
    | Scala 2.13.3   | ✅   | ✅              | ☠️                       |
    | Scala 3.0.0-M1 | ✅   | ✅              | ☠️                       |
    | Dotty 0.27     | ✅   | ☠️<sup>1</sup>  | ☠️                       |

  There's a problem with running MUnit on Scala.js with Dotty 0.27, so those tests are disabled.

* Github Actions is used for CI and Releases

   * On pushes and pull requests, `sbt ci` command is ran (more about it later)
   * On tags, `sbt ci-release` command is ran, from [sbt-ci-release](https://github.com/olafurpg/sbt-ci-release)
   * Version is determined using [sbt-dynver](https://github.com/dwijnand/sbt-dynver)

* Syntax formatting is verified using [sbt-scalafmt](https://github.com/scalameta/sbt-scalafmt)

* Imports are organised and checked using [organize-imports](https://github.com/liancheng/scalafix-organize-imports) Scalafix rule

  * Several other Scalafix rules are enabled by default, see [.scalafix.conf](.scalafix.conf)

* Compilation flags are set using [sbt-tpolecat](https://github.com/DavidGregory084/sbt-tpolecat)

* Explicit dependencies are checked using [sbt-explicit-dependencies](https://github.com/cb372/sbt-explicit-dependencies)

* Presence of Licence header is checked using [sbt-header](https://github.com/sbt/sbt-header/)

* Binary incompatibilities among dependencies are checked using [sbt-missinglink](https://github.com/scalacenter/sbt-missinglink)

* Build matrix is managed using [sbt-projectmatrix](https://github.com/sbt/sbt-projectmatrix)

### `sbt preCI`

A `preCI` command is added - which will reformat, apply scalafix rules, create licence headers, run missinglink, etc.

This command is designed to be run before pushing, **not on CI**.

`sbt ci` command only runs checks, it never changes sources.
