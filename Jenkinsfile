@Library('libpipelines') _

hose {
    EMAIL = 'conectores'
    UPSTREAM_VERSION = '5.1.42'
    VERSIONING_TYPE = 'stratioVersion-3-3'
    DEVTIMEOUT = 60
    RELEASETIMEOUT = 60
	@@ -12,4 +14,8 @@ hose {
    ANCHORE_TEST = false
    DEPLOYONPRS = true
    LABEL_CONTROL = true

    DEV = { config ->
        doDeploy(config)
    }
}