In erlang an application is considered a unit that is responsible for a functionality
and can be started and stopped as a unit.

An application follows the application specification. It specification resides in an
application resource file with the extension `.app`.

The application works following the OTP design principles[1], thus exports
pre-defined functions so that the unit can be started and stopped by the system/supervisor.

---

Application.load(AppName) loads the application in the currnet application controller, it does
not start eht application. It can also be configured to be distributed across nodes.

Application.start(AppName[, Type]) loads and starts the application, if not already loaded.
This also starts the umbrella of applications recursively. If the application cannot start it returns
{error, {not_started, AppName}}

The application controller creates an application master for the application. It is the group leader
for the processes started by the application.

The Type of application is the restart_type. It is default temporary, can also be transient and
permanent. If a transient application is terminated normally, the other applications are not
terminated. When terminated abnormally, the other applications are terminated, and also the node.
When a permanent application terminates, all other applications and node are terminated.


---

Then the application callback module has to be implemented to be able to start an application.

start, start_phase, prep_stop, stop, config_change are such callback functions.



---

refs

[1] http://www.erlang.org/doc/design_principles/des_princ.html
