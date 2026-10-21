# Changelog

## [0.10.0](https://github.com/mhalavach/rapira/compare/v0.9.1...v0.10.0) (2026-10-21)


### ⚠ BREAKING CHANGES

* remove the over-engineering stuff
* remove the dynamic and ondemand pool scaling
* the pool table rejects `scaling`, `min_spare`, `max_spare` and `process_idle_timeout_secs` as unknown fields.
* **grpc:** add the keepalive keys and simplify the host code
* **grpc:** Plugin::php() returns PhpPart, PhpPart::dispatcher is not an Option, run_plugin takes the Stopper, and Rapira::start_worker returns Rapira.
* remove the test-only API and run the tests on the rapira binary
* remove the test-only API and run the tests on the rapira binary
* **grpc:** the `Interceptor` type and the `interceptor` module leave the public API of rapira_grpc, and `[grpc].interceptors` now fails the boot as an unknown key.
* **sapi:** make the WorkerHooks callbacks required
* **sapi:** remove the class_exists and class_extends probes
* **sapi:** remove the channel route of Intake and Sink
* **sapi:** remove Rapira::start and its private scoreboard
* **grpc:** remove the test-only server and call API
* **http:** remove the test-only server API
* **net:** let Acceptor::adopt take the stop flag
* **sapi:** drop the entrypoint and mode fields from Worker
* **grpc:** let Plugin::modes be the one pool mode rule
* carry the drain grace in Worker and name the plugin in place of host and front
* **http,grpc:** run [http].middleware and [grpc].interceptors as tower layers
* **config:** let each plugin own its config section
* **grpc:** own the Rapira\Grpc PHP surface in the grpc plugin crate
* **http:** own the Rapira\Http PHP surface in the http plugin crate
* **build:** add rapira_php_build and register plugin classes through a MINIT registry
* **sapi:** replace Extension, ExtensionRuntime and Backend with Plugin, Work and Intake
* **sapi:** carry work units through one intake and set the dispatcher classes per worker
* **sapi:** fold extension_api and rapira_runtime into rapira_sapi and delete the mirror types
* **sapi:** rename php_sys to rapira_sapi and move the listener types to net
* **grpc:** extension_api::Backend has a new required method, unary(). \Rapira\Http\Tls is now \Rapira\Tls. The [http] table is optional.
* [pool] is now [http.pool]; --config, --processes, --mode, --listen, and the SCRIPT argument are removed.

### Features

* add argv at boot on PHP 8.4 with register_argc_argv off ([f62d84f](https://github.com/mhalavach/rapira/commit/f62d84fc943687794ea4cf62eb111e363c0d331c))
* add pre-built PHP extensions ([6a3fb9f](https://github.com/mhalavach/rapira/commit/6a3fb9fb512a47c9e82df1a5821a6d4dfdeed906))
* add pre-built PHP extensions ([677395d](https://github.com/mhalavach/rapira/commit/677395d69ee499db139843c2ced4d5f03c1af54c))
* adopt release-please ([f459164](https://github.com/mhalavach/rapira/commit/f45916485e92f665f416f258f86b2e5136834be7))
* adopt release-please ([1718e74](https://github.com/mhalavach/rapira/commit/1718e74961c5aac4ed68936f2bb22971c77bd868))
* **build:** add rapira_php_build and register plugin classes through a MINIT registry ([545be18](https://github.com/mhalavach/rapira/commit/545be185cfbc3e271462f89823196262032e5b3b))
* count requests that fail on a full worker queue ([9e9395a](https://github.com/mhalavach/rapira/commit/9e9395a17e8b57f2f28f83413123af830618e98a))
* Docker packages ([b333738](https://github.com/mhalavach/rapira/commit/b333738910571503b17be12034bce7a4d24eb20d))
* fill $_SERVER at boot in worker and dispatcher mode ([f159954](https://github.com/mhalavach/rapira/commit/f1599544d074dd8bb7df288e3d3c5ac80e89e609))
* fill $_SERVER at boot in worker and dispatcher mode ([3eba87d](https://github.com/mhalavach/rapira/commit/3eba87dd01bd2b7c2b6b168fb9d110893ae50b36)), closes [#129](https://github.com/mhalavach/rapira/issues/129)
* getMode implementation ([95ddc12](https://github.com/mhalavach/rapira/commit/95ddc12fa236e7090971f0d8bddf11ae8298e1de))
* getMode implementation ([#95](https://github.com/mhalavach/rapira/issues/95)) ([6d979dd](https://github.com/mhalavach/rapira/commit/6d979dd10914957ff13d9aa6b0344570e41e63b3))
* **grpc:** add interceptors with a built-in auth interceptor ([ff72a0d](https://github.com/mhalavach/rapira/commit/ff72a0d6f337fbef2ce700ab77f10e7ea0ae82fb))
* **grpc:** add the auth interceptor crate ([2ff4ea0](https://github.com/mhalavach/rapira/commit/2ff4ea0969e7d37647d9aa9488b13f0ae9e72109))
* **grpc:** add the keepalive keys and simplify the host code ([ac56141](https://github.com/mhalavach/rapira/commit/ac56141af8c1dadf83cd750b7f522b06155d198d))
* **grpc:** add the keepalive keys and simplify the host code ([3c31d67](https://github.com/mhalavach/rapira/commit/3c31d670339526b9760cdbc78c4501ef3ae96cbe))
* **grpc:** run [grpc].interceptors with the auth interceptor ([0e7a310](https://github.com/mhalavach/rapira/commit/0e7a3100c71a028695b6039a8568680b9098f28b))
* **grpc:** serve unary RPCs from PHP through ConnectRPC ([4f4d1b0](https://github.com/mhalavach/rapira/commit/4f4d1b03a562fd7162f6e16289234edddc5cfdc9))
* **grpc:** serve unary RPCs from PHP through ConnectRPC ([#132](https://github.com/mhalavach/rapira/issues/132)) ([fbaeb30](https://github.com/mhalavach/rapira/commit/fbaeb30a1a8a3dc20bb7651037e967261f6d4db0))
* **http,grpc:** run [http].middleware and [grpc].interceptors as tower layers ([a15adb4](https://github.com/mhalavach/rapira/commit/a15adb463501af82078a56c9fed64f1419f78963))
* **http:** expose server_name and server_port on HttpDispatcherInfo ([0a18793](https://github.com/mhalavach/rapira/commit/0a1879311be015e6f9dd0670baafb4b5d055e4dd))
* **http:** expose server_name and server_port on HttpDispatcherInfo ([ca32802](https://github.com/mhalavach/rapira/commit/ca328021dc6fdbfb467d2e6aa1710c64eca63808))
* hyper based http impl ([162df2d](https://github.com/mhalavach/rapira/commit/162df2d1614fe0ac0869a52d992ef0ea2f5ef404))
* implement fibers, multipart and more of the Request ([5d70b64](https://github.com/mhalavach/rapira/commit/5d70b649a36462506be4aac90a255741842d1bb9))
* implement more dispatcher classes ([98c6044](https://github.com/mhalavach/rapira/commit/98c604470391daa79a30583cb9ad490835032f6d))
* **master:** count worker exits per verdict in the scoreboard ([916d777](https://github.com/mhalavach/rapira/commit/916d7778419a9b323f7a4852640d717d04ffaa2f))
* **master:** give every child the whole board and the pool regions ([8a37906](https://github.com/mhalavach/rapira/commit/8a37906c1845be659cb42c9a928798d991a012b3))
* **metrics:** add the Prometheus text endpoint crate ([93d392e](https://github.com/mhalavach/rapira/commit/93d392eb49483723c5fdf8060e64977b64dfc716))
* **metrics:** make the idle keep-alive timeout configurable ([74648fe](https://github.com/mhalavach/rapira/commit/74648fe86a2de30141bf81a89a7d01fcf2b9814b))
* more C files, add dispatcher PHP classes bindings ([335e1a7](https://github.com/mhalavach/rapira/commit/335e1a76a037319a9f005c1476dc85992f58fd4c))
* **observability:** serve the livez and readyz probes ([2033519](https://github.com/mhalavach/rapira/commit/203351990d847b519322466d7216d60482197f23))
* per-connection PHPHandler ([5d188a0](https://github.com/mhalavach/rapira/commit/5d188a0718a3da57f07b9a04f2b850b156e7b1b7))
* per-connection PHPHandler ([9c5f2ec](https://github.com/mhalavach/rapira/commit/9c5f2ec17a42489fed0189cb8d3cfd604c7f4147))
* **sapi:** count queue-full sheds as failed units ([e637caa](https://github.com/mhalavach/rapira/commit/e637caa6aa2ce4b809bb59206eba80fe8529ac00))
* **sapi:** count the worker queue in the scoreboard slot ([649f63d](https://github.com/mhalavach/rapira/commit/649f63d4752878f800d85134e2679bbe97182347))
* **scoreboard:** keep slot counters across worker respawns ([4248664](https://github.com/mhalavach/rapira/commit/42486641d2958a64abd8f649971b2aa578961428))
* sendFile, streams, timeouts ([90d6c1e](https://github.com/mhalavach/rapira/commit/90d6c1ee32190779fbfc0b4cdf572bd957037ff9))
* serve Prometheus metrics and the livez and readyz probes ([5dc0632](https://github.com/mhalavach/rapira/commit/5dc063244d5715eb082af0777cf91f8b9eea2d72))
* serve Prometheus metrics from a [metrics] listener ([9def9d7](https://github.com/mhalavach/rapira/commit/9def9d7b98f63777bcd8d83f067750f01f584ecc))
* static files cache ([dba6f55](https://github.com/mhalavach/rapira/commit/dba6f55003b81785c99a39c61cb2756d1160172d))
* static files cache ([de94729](https://github.com/mhalavach/rapira/commit/de9472908f165ecdcc777c3aabcb83d25f3b1c31))
* static files serving ([#76](https://github.com/mhalavach/rapira/issues/76)) ([#96](https://github.com/mhalavach/rapira/issues/96)) ([b4cf362](https://github.com/mhalavach/rapira/commit/b4cf362e2125d254a477f2ae95f2fd19276455eb))
* worker pool per plugin ([aca6755](https://github.com/mhalavach/rapira/commit/aca67556c47d44946d3415390818c674269afeb8))
* worker pool per plugin ([#104](https://github.com/mhalavach/rapira/issues/104)) ([4778798](https://github.com/mhalavach/rapira/commit/4778798b6e5f02f2d8a448a75e4e491b26a62139))


### Bug Fixes

* build against PHP 8.7 without the removed SAPI methods ([f41ff1d](https://github.com/mhalavach/rapira/commit/f41ff1dca5c2dd9f694ff93de98f8e732f227771))
* build against PHP 8.7 without the removed SAPI methods ([4fd82d6](https://github.com/mhalavach/rapira/commit/4fd82d63a9be2ce3050c2fb156b9942a610e08f4))
* classic mode speedup ([5670520](https://github.com/mhalavach/rapira/commit/5670520f58fdfb4b83eddc29d474437dd9282dd8))
* classic mode speedup ([abae8d3](https://github.com/mhalavach/rapira/commit/abae8d3a366a3631a09395fac1ef55ac45cc1f0a))
* close the other pools' listeners in a forked child ([4a30325](https://github.com/mhalavach/rapira/commit/4a303250b572024fe395239986163bb67ce0b098))
* copy the libraries of libphp.so into the Linux release ([db82240](https://github.com/mhalavach/rapira/commit/db82240af52a57cd4170a095306f2d874e4e12a9))
* copy the libraries of libphp.so into the Linux release ([62206bf](https://github.com/mhalavach/rapira/commit/62206bf04a9cbdffcabb98f7803e367aa194136a)), closes [#207](https://github.com/mhalavach/rapira/issues/207)
* disable transparent huge pages in the master and the workers ([a9aa4a9](https://github.com/mhalavach/rapira/commit/a9aa4a9171f17a717c942e615571b64d339a3d58))
* disable transparent huge pages in the master and the workers ([a5f5af1](https://github.com/mhalavach/rapira/commit/a5f5af1dca4fc3db0fdb77c79453a426b3c1de32)), closes [#151](https://github.com/mhalavach/rapira/issues/151)
* **dispatcher:** allow receive after observed cancellation ([521d97b](https://github.com/mhalavach/rapira/commit/521d97b85401a0f03329914fcc8498e86c9dd01e))
* **dispatcher:** log the discard of an abandoned exchange ([53a3615](https://github.com/mhalavach/rapira/commit/53a3615aa8f507de238b42c97a571dcbda333804))
* fix php 8.6 send_header_fcc ([6c9bd72](https://github.com/mhalavach/rapira/commit/6c9bd729caaf3ab2862db3881cf5dabae85b1619))
* **fuzz:** lock bindgen to syn 3 again ([88544d1](https://github.com/mhalavach/rapira/commit/88544d1bf70d6b2689930740b67b30c05e4c762a))
* **grpc:** keep the status of a gRPC error in the trailers only ([2afbc11](https://github.com/mhalavach/rapira/commit/2afbc11c4e48e90fd8c61c943c4f8a4549d95bbb))
* **grpc:** reject a descriptor set that lacks an imported file ([7add905](https://github.com/mhalavach/rapira/commit/7add905f8f7d5b2b1ef72e84f5e98872c93f97ad))
* HASH_KEY_IS_STRING global var to handle diff between 8.4 and 8.5 ([bf69b25](https://github.com/mhalavach/rapira/commit/bf69b2521833c360002048a74239dd527f807a39))
* **http:** arm the delivery watermark behind body-mapping middleware ([fef1338](https://github.com/mhalavach/rapira/commit/fef133863b6d1144328a6402652b7c93a5ee3318))
* **http:** cancel PHP only when a completed response was never flushed ([1ffb8f5](https://github.com/mhalavach/rapira/commit/1ffb8f51578ebd7da8fe555522363eeb10cf71c5))
* **http:** cap the body reservation at max_body_size ([1cd460d](https://github.com/mhalavach/rapira/commit/1cd460d3f1f92fcaf21151117ca9666f46ad18b0))
* **http:** correct exchange completion and cancellation ([b84aa72](https://github.com/mhalavach/rapira/commit/b84aa72d89c8ac4ed7d011cde269912bb3e789ce))
* **http:** frame no-body responses as empty for the delivery watermark ([a52cb77](https://github.com/mhalavach/rapira/commit/a52cb775a477ea8a550183aee9618077284bd885))
* **http:** improve connection distribution across workers ([485242a](https://github.com/mhalavach/rapira/commit/485242aafa6c4122f20560d3ee729a21b770fec9))
* **http:** improve connection distribution across workers ([52dc11f](https://github.com/mhalavach/rapira/commit/52dc11f21979118e8fa32936fc2343bcc8ab0d53))
* **http:** preserve exchanges after content-length completion ([4ff03e5](https://github.com/mhalavach/rapira/commit/4ff03e5762eb1f3d9532294877b3064ec377a736))
* **http:** rotate after a failed accept and end the loop on a failed rotation ([2580a4e](https://github.com/mhalavach/rapira/commit/2580a4e32b1c968b8467a5ff3ca3299007330b61))
* **master:** keep a booted pool up when one worker never boots ([582a992](https://github.com/mhalavach/rapira/commit/582a9924af24c1bcdf564c084ecbf9a913dbdd0b))
* **master:** keep an ondemand pool armed while it reloads ([1d35f8f](https://github.com/mhalavach/rapira/commit/1d35f8fffdbe8712c3ebf718bf63daeac0518777))
* **master:** let workers drain when the master dies ([16b19d1](https://github.com/mhalavach/rapira/commit/16b19d14d8dedecd927784272495a24ac73712c0))
* **master:** run the request watchdog while a pool reloads ([2974915](https://github.com/mhalavach/rapira/commit/2974915bd301a1c5809c8e5bf0fac4f841ae6e11))
* on php 8.6 XtOffsetOf was replaced by offsetof ([33b087c](https://github.com/mhalavach/rapira/commit/33b087c5525bdae7907e42c380caa088dbb51612))
* pin Rust 1.98.1 ([#201](https://github.com/mhalavach/rapira/issues/201)) ([49c395f](https://github.com/mhalavach/rapira/commit/49c395f770049ba03f23b3c88a69db7404e0be44))
* pin Rust 1.98.1 and align the build versions ([85eeae6](https://github.com/mhalavach/rapira/commit/85eeae62d0f7c07dbbbce14be737889acf1fde68))
* probe the sendfile root at boot and pin the debug profile to one worker ([52bebef](https://github.com/mhalavach/rapira/commit/52bebefc30dafa598e88aada335475acdcb00caf))
* register shutdown functions (boot) once ([6cce535](https://github.com/mhalavach/rapira/commit/6cce535fd4e74cd67432378c21a417cce60a83d9))
* **release:** bundle macOS dylibs that load through [@loader](https://github.com/loader)_path ([2fb1811](https://github.com/mhalavach/rapira/commit/2fb1811e56d40a59f231a4c4507fd927cc50b48e))
* **release:** package OPcache for PHP 8.4 ([f8ba5b4](https://github.com/mhalavach/rapira/commit/f8ba5b4d272439b2a8519f55fa01837fe8040777))
* removed log class bindings by mistake ([3f5eab0](https://github.com/mhalavach/rapira/commit/3f5eab002f3d4f6e456b405530719731f7522d45))
* **sapi:** keep a failed boot starting in the shed pull ([ec35cd1](https://github.com/mhalavach/rapira/commit/ec35cd122c97f33143714068f602710f915d15e9))
* **sapi:** mark a failed boot cycle starting ([bb8e7a4](https://github.com/mhalavach/rapira/commit/bb8e7a4f80f47263188d494effa8945c25ce5ba7))
* **sapi:** run a failed boot again when no request arrives ([260bb2a](https://github.com/mhalavach/rapira/commit/260bb2abbf63f58648f5dd24d1e959fd51112e49))
* **sapi:** show draining after a failed boot cycle of a draining worker ([ca66db1](https://github.com/mhalavach/rapira/commit/ca66db14bdfe452b5a5e91219843844fc17b961e))
* **scoreboard:** keep a worker starting until its first pull ([aa0090c](https://github.com/mhalavach/rapira/commit/aa0090c92da36e034f3020d976f23eebad3f112b))
* seal a teardown flush bailout as an error ([f7199ca](https://github.com/mhalavach/rapira/commit/f7199ca5cd76d8fc1d9d03c00efd923b372752ef))
* tests (new mode name), rapira modes ([495cd9e](https://github.com/mhalavach/rapira/commit/495cd9e3bd5586a26c06af5fb9f437439fb1edff))
* **worker:** preserve retained SPL temporary streams ([2e28c19](https://github.com/mhalavach/rapira/commit/2e28c19b7459fb65faf558ce44aea24f65a29462))
* **worker:** preserve retained SPL temporary streams ([b0e4ff6](https://github.com/mhalavach/rapira/commit/b0e4ff63e9053c3ae8ea4cf1777d0ffa685fc256))


### Performance Improvements

* **api:** carry headers as HeaderMap end to end ([7a8fd31](https://github.com/mhalavach/rapira/commit/7a8fd3150665e79fffb559a79ef62f9d7fc07e96))
* **classic:** drop the per-request entrypoint probe ([8626757](https://github.com/mhalavach/rapira/commit/862675766e8966e84bdad0f902062e7e6b92b954))
* **http,grpc:** serve the empty interceptor chain unboxed and spawn connections without a box ([d23d0dd](https://github.com/mhalavach/rapira/commit/d23d0ddc3fa31bb041680bf4a7182d4630751b2a))
* **http:** arm request timers only when the awaited future is pending ([70fdfd3](https://github.com/mhalavach/rapira/commit/70fdfd33cfead6597331a8cb279969524bbd9805))
* **http:** block in epoll_wait so EPOLLEXCLUSIVE wakes one worker ([3c13465](https://github.com/mhalavach/rapira/commit/3c134657857d639eaa7b5d7a165610fe9f191030))
* **http:** build the CGI view on the transport thread and serve every connection unboxed ([6ae917d](https://github.com/mhalavach/rapira/commit/6ae917d38bf953ec01339cfa67dde5b01b2dad75))
* **http:** consume a queued End at body drop ([18d09d0](https://github.com/mhalavach/rapira/commit/18d09d0043262bd1e6b7cbb3cf157b37b53d8c9f))
* **http:** consume a queued End before the drain task spawns ([0cdd977](https://github.com/mhalavach/rapira/commit/0cdd977a9c3ccd3973adf4e1a93ab2abaeb86a9c))
* **http:** count flushes without a watch notification ([e8e1c15](https://github.com/mhalavach/rapira/commit/e8e1c1567460289e451b59a7b0f54eda420f82c8))
* **http:** cut copies when the request is built ([0ea1180](https://github.com/mhalavach/rapira/commit/0ea118060b06b69ad3e3bacad2d7559fb9060165))
* **http:** skip hop-by-hop removal when the response has no such field ([31c6c93](https://github.com/mhalavach/rapira/commit/31c6c934dc7395302ea31271fff8f306f7a129ce))
* **http:** wake one worker per connection and trim the classic request path ([6dd6a1e](https://github.com/mhalavach/rapira/commit/6dd6a1e5b7e1ce0c9363e07aa49ed62d40a9fd83))
* **http:** write getRequest() properties by slot and drop fmt from the view ([03f499e](https://github.com/mhalavach/rapira/commit/03f499efe167934a3832bae34ed9b2ea6a736292))
* **php_sys:** build the Request view on the first getRequest() ([b663fb3](https://github.com/mhalavach/rapira/commit/b663fb3f81518e6bdf33ac2483fcd8778c9b9778))
* **php_sys:** carry boxed jobs through the intake channel ([93cbb26](https://github.com/mhalavach/rapira/commit/93cbb262092403fe7318e8809ea9b7c0b76e9faa))
* **php_sys:** drop per-request work on the response and log paths ([1966b42](https://github.com/mhalavach/rapira/commit/1966b42ca37b26115f2829e78e0799573ffd1f99))
* **php_sys:** fold request headers in place for superglobals ([e14b673](https://github.com/mhalavach/rapira/commit/e14b673f9da4b909eac01c8a22bf4c43868144ad))
* **php_sys:** hold the script paths once per worker ([4cc3acf](https://github.com/mhalavach/rapira/commit/4cc3acf7909e1aa1a12c0a939157a68aa33e8262))
* **sapi:** append the digits of push_dec in one call ([5786159](https://github.com/mhalavach/rapira/commit/5786159a1725a86130d554bdf1f76b65475f126a))
* **sapi:** register $_SERVER through php_register_known_variable ([00e4b17](https://github.com/mhalavach/rapira/commit/00e4b17f763a00ddb0f973ff8dcba06bfd241db8))
* **sapi:** skip the timer disarm in receive() when a job is queued ([33b5c12](https://github.com/mhalavach/rapira/commit/33b5c120d7420d554471c4c44edd4735de75ab13))
* **sapi:** wait for the plugin thread on a condvar ([a412c9f](https://github.com/mhalavach/rapira/commit/a412c9f9bd008b512dd2398f6430fc62b3677bd2))
* trim the request path and drop dead code across the workspace ([a36a356](https://github.com/mhalavach/rapira/commit/a36a356f8bbf9af5fb93c938636372de3c6f062e))
* **worker:** keep the working directory across classic requests ([ac1e9bc](https://github.com/mhalavach/rapira/commit/ac1e9bc3e8f986da275243a1389cccf14cb69bc8))


### Miscellaneous Chores

* remove the dynamic and ondemand pool scaling ([0cafb5b](https://github.com/mhalavach/rapira/commit/0cafb5bc963ff2405c9c68eb756c750bcd586816))
* remove the dynamic and ondemand pool scaling ([6845efc](https://github.com/mhalavach/rapira/commit/6845efc2bb4a7bfdbdee8effffd41759945ea1a9))


### Code Refactoring

* carry the drain grace in Worker and name the plugin in place of host and front ([e0fe15b](https://github.com/mhalavach/rapira/commit/e0fe15b1acf8239c308fcc5742aa165c7aca210b))
* **config:** let each plugin own its config section ([8bad96c](https://github.com/mhalavach/rapira/commit/8bad96c8ade346b5dcba1a3645b366c501a4243e))
* **grpc:** let Plugin::modes be the one pool mode rule ([b1ef9c2](https://github.com/mhalavach/rapira/commit/b1ef9c2ba8aab4bbeec7385100eb76aec264a0a6))
* **grpc:** own the Rapira\Grpc PHP surface in the grpc plugin crate ([36f44d6](https://github.com/mhalavach/rapira/commit/36f44d6079b5f6fd62ecfe8133251fd8afeb8526))
* **grpc:** remove the interceptor path that no config can fill ([ba520bb](https://github.com/mhalavach/rapira/commit/ba520bbf06df9fbaacd9f6e79afc2eda9ad232c7))
* **grpc:** remove the test-only server and call API ([ca86c42](https://github.com/mhalavach/rapira/commit/ca86c42b3350564420500e7a82199856475fccb1))
* **http:** own the Rapira\Http PHP surface in the http plugin crate ([9d54d07](https://github.com/mhalavach/rapira/commit/9d54d07ec0729efd817d24125c197e0afe54f883))
* **http:** remove the test-only server API ([c540f25](https://github.com/mhalavach/rapira/commit/c540f25565ffb3e657ec68eb940a23f5e1c4755b))
* **net:** let Acceptor::adopt take the stop flag ([291c3f0](https://github.com/mhalavach/rapira/commit/291c3f05ee7610f63ae7b6bf4e103866daf818cb))
* remove the over-engineering stuff ([13ad6f3](https://github.com/mhalavach/rapira/commit/13ad6f385c1660cfb93bbd8b42afeb251d397c03))
* remove the test-only API and run the tests on the rapira binary ([4f0846e](https://github.com/mhalavach/rapira/commit/4f0846e4057dbff190163312b6ddb82742f7a791))
* remove the test-only API and run the tests on the rapira binary ([4f0846e](https://github.com/mhalavach/rapira/commit/4f0846e4057dbff190163312b6ddb82742f7a791))
* **sapi:** carry work units through one intake and set the dispatcher classes per worker ([be3dd06](https://github.com/mhalavach/rapira/commit/be3dd068ebd949215710e6e71d19ce13ea6f9ddd))
* **sapi:** drop the entrypoint and mode fields from Worker ([86601a4](https://github.com/mhalavach/rapira/commit/86601a497d56cdb3e3b25f407bf86e17e9f587b8))
* **sapi:** fold extension_api and rapira_runtime into rapira_sapi and delete the mirror types ([91cc60b](https://github.com/mhalavach/rapira/commit/91cc60bcd39323a9f4dfb1e30097940c4c8ab59b))
* **sapi:** make the WorkerHooks callbacks required ([2d6d539](https://github.com/mhalavach/rapira/commit/2d6d5392aed71340c540ef1c92068bf9cd2e2661))
* **sapi:** remove Rapira::start and its private scoreboard ([d786d23](https://github.com/mhalavach/rapira/commit/d786d23eb08e40726a51ae85ec058ed29b725283))
* **sapi:** remove the channel route of Intake and Sink ([cd743e4](https://github.com/mhalavach/rapira/commit/cd743e4ef53d99236b48e7e08bdb48b9345d02d8))
* **sapi:** remove the class_exists and class_extends probes ([e3c8810](https://github.com/mhalavach/rapira/commit/e3c88100886e98123a61e37f461d32208c384ad3))
* **sapi:** rename php_sys to rapira_sapi and move the listener types to net ([88b7b77](https://github.com/mhalavach/rapira/commit/88b7b77415047d29be5dacad1fd100d11059f957))
* **sapi:** replace Extension, ExtensionRuntime and Backend with Plugin, Work and Intake ([44c4ebe](https://github.com/mhalavach/rapira/commit/44c4ebe7d3014fb95abead1e7be956da243ef394))

## [0.9.1](https://github.com/rapira-rs/rapira/compare/v0.9.0...v0.9.1) (2026-10-07)

### 🎯 Core

- 🐛 **Work State Checks**: Fixed worker crashes after `isCancelled()` or `isFinalized()` calls in x86_64 release builds. The builds use Rust 1.98.1 until a Rust release fixes the compiler defect, BUG [#201](https://github.com/rapira-rs/rapira/issues/201) (thanks @roxblnfk).

### 📦 `http` plugin

- 🐛 **HTTP/1.1 Headers**: Responses with `Transfer-Encoding` no longer send `Content-Length`. A `close` token in any `Connection` request header closes the connection, even when a later one says `keep-alive`, [#202](https://github.com/rapira-rs/rapira/pull/202).

### 📦 PHP Packages

- 🧹 **Docker Images**: Updated the PHP base images to 8.5.11 and 8.4.26, [#202](https://github.com/rapira-rs/rapira/pull/202).
- 🧹 **macOS Archives**: The macOS archive requires macOS 26 or later. It bundles the Homebrew libraries of the `macos-latest` build runner, [#202](https://github.com/rapira-rs/rapira/pull/202).

## [0.9.0](https://github.com/rapira-rs/rapira/compare/v0.8.1...v0.9.0) (2026-10-05)

### 🎯 Core

- ✨ **Plugin Worker Pools**: Added independent worker pools under `[http.pool]` and `[grpc.pool]`, FR [#104](https://github.com/rapira-rs/rapira/issues/104).
- 🧹 **Pool Configuration**: Each pool runs a fixed `processes` count. The server command is `rapira serve <CONFIG>`, [#149](https://github.com/rapira-rs/rapira/issues/149), [#116](https://github.com/rapira-rs/rapira/pull/116).
- ✨ **Worker Boot Environment**: Added process environment values, script paths, `argv`, and `argc` to `$_SERVER` at worker and dispatcher boot, FR [#129](https://github.com/rapira-rs/rapira/issues/129) (thanks @FluffyDiscord).
- 🧹 **Plugin API**: Consolidated the PHP runtime in `rapira_sapi` and simplified the Rust plugin API. Each plugin owns its PHP classes and configuration, [#144](https://github.com/rapira-rs/rapira/pull/144), [#145](https://github.com/rapira-rs/rapira/pull/145), [#194](https://github.com/rapira-rs/rapira/pull/194).
- 🐛 **Worker Memory**: Disabled transparent huge pages on Linux to reduce worker memory use, [#151](https://github.com/rapira-rs/rapira/issues/151).
- 🐛 **Temporary Streams**: Kept retained `SplTempFileObject` streams usable across worker requests, [#111](https://github.com/rapira-rs/rapira/pull/111).
- 🐛 **Worker Lifecycle**: Workers can drain active requests after the master exits unexpectedly. The request watchdog stays active during pool reloads, [#130](https://github.com/rapira-rs/rapira/pull/130), [#116](https://github.com/rapira-rs/rapira/pull/116).

### 📦 `http` plugin

- ⚡ **Request Performance**: Reduced request copies, allocations, and system calls. On Linux, one waiting worker wakes for each new connection, [#127](https://github.com/rapira-rs/rapira/pull/127), [#130](https://github.com/rapira-rs/rapira/pull/130).
- 🧹 **Classic Working Directory**: Classic workers keep their working directory across requests, so a `chdir()` applies until the worker exits, [#127](https://github.com/rapira-rs/rapira/pull/127).
- 🐛 **Exchange Completion**: Fixed false cancellation after a complete response. Dispatchers can accept new work after client cancellation, [#113](https://github.com/rapira-rs/rapira/pull/113).

### 📦 `grpc` plugin

- ✨ **Unary RPCs**: Added PHP handlers for gRPC, binary gRPC-Web, and Connect with protobuf or JSON messages. Includes health checks and optional server reflection, FR [#132](https://github.com/rapira-rs/rapira/issues/132).
- ✨ **Authentication**: Added interceptor chains and a built-in bearer-token check before calls reach PHP, FR [#36](https://github.com/rapira-rs/rapira/issues/36).
- ✨ **HTTP/2 Keepalive**: Added `keepalive_interval_secs` and `keepalive_timeout_secs` to `[grpc]`, [#148](https://github.com/rapira-rs/rapira/pull/148).

### 📊 Observability

- ✨ **Prometheus Metrics**: Added `/metrics` for worker state, requests, queues, exits, and Linux memory use. Counters persist across worker respawns, FR [#83](https://github.com/rapira-rs/rapira/issues/83) (thanks @Zylius).
- ✨ **Health Probes**: Added `/livez` and `/readyz` for master liveness and PHP pool readiness, FR [#49](https://github.com/rapira-rs/rapira/issues/49) (thanks @rauanmayemir).
- 🧹 **Log Timestamps**: JSON logs include microseconds in `timestamp`, [#194](https://github.com/rapira-rs/rapira/pull/194).

### 📦 PHP Packages

- ✨ **Pre-built Extensions**: Added `pdo_pgsql`, `pgsql`, `bcmath`, `intl`, `igbinary`, and `redis` to release builds and Docker images, FR [#103](https://github.com/rapira-rs/rapira/issues/103) (thanks @FluffyDiscord).
- 🐛 **Release Bundles**: Included OPcache in PHP 8.4 packages and required shared libraries in macOS archives, [#117](https://github.com/rapira-rs/rapira/pull/117), [#130](https://github.com/rapira-rs/rapira/pull/130).
- 🐛 **PHP 8.7 Builds**: Fixed builds against PHP 8.7 development headers, [#156](https://github.com/rapira-rs/rapira/pull/156).

## [0.8.1](https://github.com/rapira-rs/rapira/compare/v0.8.0...v0.8.1) (2026-09-05)

### 🎯 Core

- 🐛 **Connection Distribution**: Improved distribution of new HTTP connections across workers on Linux for TCP and Unix sockets, BUG [#107](https://github.com/rapira-rs/rapira/issues/107) (thanks @FluffyDiscord).

## [0.8.0](https://github.com/rapira-rs/rapira/compare/v0.7.0...v0.8.0) (2026-09-02)

### 🎯 Core

- ✨ **Hyper HTTP Server**: Replaced the Pingora HTTP layer with a Hyper and Tower HTTP/1.1 server. Added a shared middleware interface, FR [#35](https://github.com/rapira-rs/rapira/issues/35).
- ✨ **Runtime Mode API**: Added `\Rapira\Mode` and `\Rapira\get_mode()` for Classic, Worker, and Dispatcher modes. Renamed `NotInWorkerModeError` to `NoDispatcherError`, FR [#77](https://github.com/rapira-rs/rapira/issues/77) (thanks @roxblnfk).
- ✨ **PHP Handler Lifetime**: Built one `PHPHandler` for each connection and separated per-request state, FR [#99](https://github.com/rapira-rs/rapira/issues/99).
- 🐛 **Worker Shutdown**: Stopped the per-request destructor sweep. Boot shutdown functions now run once when the worker exits. Long-lived boot objects remain usable across requests, BUG [#82](https://github.com/rapira-rs/rapira/issues/82) (thanks @Zylius).

### 📦 `static_files` middleware

- ✨ **Static File Serving**: Added configurable static file serving. File misses continue to PHP, FR [#76](https://github.com/rapira-rs/rapira/issues/76).
- ✨ **Static File Cache**: Added a per-worker memory cache with one-second revalidation, a 16 MiB capacity, and a 256 KiB limit for each file, FR [#98](https://github.com/rapira-rs/rapira/issues/98).
