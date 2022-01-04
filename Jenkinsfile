
ci 'ecs-global-slave', {

    env.group = "aura"
    env.team = "orange"
    env.subteam = "infra"
    env.language = "javascript"
    env.service_name = "db-migrate-mysql"
    env.service_git_repo = "${env.service_name}"

    String version_type_minor = "minor", version_type_major = "major", version_type_patch = "patch"
    String develop_branch = "develop"

    checkout scm

    // This section will run on push to feature branch
    feature {
        auraNpm.install()
        //auraNpm.unitest("test")
    }

    // This section will run on push/merge to develop/integration branch
    pullrequest {
        auraNpm.install()
        //auraNpm.unitest("test")
    }

    //This section will run after merge was performed to develop
    develop {
        //auraNpm.install()
        auraNpm.unitest("test")

        auraGit.checkoutBranch(develop_branch)
        auraNpm.bumpNpmVersion(version_type_patch)
    }

    // This section will run on push/merge to release/hotfix/master branch
    production {
        auraNpm.install()
        //auraNpm.unitest("test")

        auraNpm.publishNpmModuleToArtifactory()
    }
}
