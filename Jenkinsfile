

@Library('libpipelines') _

hose {
    EMAIL = 'conectores'
    UPSTREAM_VERSION = '8.3.0'
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
        doPackage(conf: config)
        doGrypeScan(conf: config, artifactsList: [
                [sbom: 'target/runtime-dependencies-bom/bom.json', name: 'mysql-jdbc']
        ])
        doDeploy(conf: config)
    }
}
