# failing-job

Test case for [tilt-extensions#92](https://github.com/tilt-dev/tilt-extensions/issues/92): verify that when Tilt runs a user process via the [Restart Process extension](https://github.com/tilt-dev/tilt-extensions/tree/master/restart_process) (i.e. `docker_build_with_restart`), we ultimately return that process's exit code.

This project runs a k8s job that will always exit with code 123. With the previous version of the Restart Process extension, this failed job showed up green in the Tilt sidebar because we weren't correctly surfacing the exit code ([see snapshot of old behavior](https://cloud.tilt.dev/snapshot/AZS-w_gL231s6CjvZsA=)).

With the latest change to Restart Process, this job should correctly show up RED on the sidebar ([see snapshot of current behavior](https://cloud.tilt.dev/snapshot/AfTmw_gL772d93lJMto=)).

Instructions:
* clone this repo
* run `tilt up`
* verify that resource "failing-job" is red in the sidebar

Note: in any projects that were running into this problem with Restart Process, you'll have to `rm -rf tilt_modules/restart_process` to let Tilt fetch the updated version of the extension.
