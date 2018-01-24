## 0.0.4 (Unreleased)

IMPROVEMENTS:
 * Job types of `batch` now undergo checking to confirm the job reaches status of `running` [GH-73](https://github.com/jrasell/levant/pull/73)
 * Vendored Nomad version has been increased to 0.7.1 allowing use of Nomad ACL tokens [GH-76](https://github.com/jrasell/levant/pull/76)
 * Log messages now includes the date, time and timezone [GH-80](https://github.com/jrasell/levant/pull/80)
 
BUG FIXES: 
 * Skip health checks for task groups without canaries when performing canary auto-promote health checking [GH-83](https://github.com/jrasell/levant/pull/83)
 * Fix issue where jobs without specified count caused panic [GH-89](https://github.com/jrasell/levant/pull/89)

## 0.0.3 (23 December 2017)

IMPROVEMENTS:
 * Levant can now track Nomad auto-revert of a failed deployment [GH-55](https://github.com/jrasell/levant/pull/55)
 * Provide greater feedback around variables file passed, CLI variables passed and which variables are being used by Levant.[GH-62](https://github.com/jrasell/levant/pull/62)
 * Levant supports autoloading of default files when running `levant deploy` [GH-37](https://github.com/jrasell/levant/pull/37)

BUG FIXES:
 * Fix issue where Levant did not correctly handle deploying jobs of type `batch` [GH-52](https://github.com/jrasell/levant/pull/52)
 * Fix issue where evaluations errors were not being fully checked [GH-66](https://github.com/jrasell/levant/pull/66)
 * Fix issue in failure_inspector incorrectly handling multi-groups [GH-69](https://github.com/jrasell/levant/pull/69)

## 0.0.2 (29 November 2017)

IMPROVEMENTS:
 * Introduce `-force-count` flag into deploy command which disables dynamic count updating; meaning Levant will explicity use counts defined in the job specification template [GH-33](https://github.com/jrasell/levant/pull/33)
 * Levant deployments now inspect the evaluation results and log any error messages [GH-40](https://github.com/jrasell/levant/pull/40)

BUG FIXES:
 * Fix formatting issue in render command help [GH-28](https://github.com/jrasell/levant/pull/28)
 * Update failure_inspector to cover more failure use cases [GH-27](https://github.com/jrasell/levant/pull/27)
 * Fix a bug in handling Nomad job types incorrectly [GH-32](https://github.com/jrasell/levant/pull/32)
 * Fix issue where jobs deployed with all task group counts at 0 would cause a failure as no deployment ID is returned [GH-36](https://github.com/jrasell/levant/pull/36)

## 0.0.1 (30 October 2017)

- Initial release.
