@Library('libpipelines') _

hose {
    EMAIL = 'conectores'
    UPSTREAM_VERSION = '5.1.42'
    VERSIONING_TYPE = 'stratioVersion-3-3'
    DEVTIMEOUT = 60
    RELEASETIMEOUT = 60
    MAXITRETRIES = 2
    BUILDTOOL_IMAGE = 'stratio/connectors-maven-builder-openjdk-8:1.1.0'
    ENABLE_MAVEN_PARALLELBUILD = false
    ANCHORE_TEST = false
    DEPLOYONPRS = true
    LABEL_CONTROL = true

    DEV = { config ->
        doDeploy(config)
    }
}