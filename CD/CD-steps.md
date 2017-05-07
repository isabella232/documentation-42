# Steps for CI/CD

### Option 1: 
0. VCS clone
1. Build
    1. Compile
    2. Unit tests
    3. Publish Unit Test Report
    4. Create binary
2. Package
    1. Version
    2. Dockerize
    3. Push to Docker registry / Artifact repository
3. Dev Env
    1. Deploy to Dev Env
    2. Functional Tests
    3. Publish Functional Test Report
4. Test Env
    1. Deploy to Test Env
    2. Execut Integration Tests
    3. Publish Integration Test Report
5. Deploy to UAT Env
6. Deploy to Prod Env

### Option 2: 

1. Build
	1. Compile
2. Test 
	1. Unit tests
	2. Integration tests
	3. Sonarqube etc
3. Package/Publish	
	1. Package (war/jar etc)
	2. Version
	3. Dockerize (incase of 'push to registry')
	4. Push to registry / artifact repository
	5. Tag release (repo)
4. Deploy
	1. Dev/Test or Prod 

Generic Steps:
=============

The first build stage will use the language specific build systems e.g. maven, gradle etc. for Java, webpack, gulp, etc. for JavaScript etc.

The idea is that the first stage will be language dependent only; and rest of the stages will be common; as they will work on docker image only.

1. Build [ CIT - Continous Integration & Testing ] 
    1. Compile Code
    2. Run Tests (e.g. unit, etc.)
    3. Static Code Analysis & Test Coverage (e.g. sonarqube etc.)
    4. Generate Versioned Package (e.g. jar, war, etc.)
    5. Push Package to Artifact Repository (e.g. nexus, etc.)
    6. Create Docker Image
    7(Optional). Run Integrations Tests
    8. Push Docker Image to Docker Image Repository
2. Deploy to Dev Environment
3. Deploy to Test Environment
    1. Run different sort of tests? performance, load, etc.
4. Publish
    1. Create Release Branch
    2. Create Tag

=> Approve    

5. Deploy to Stage Environment

=> Approve?

6. Deploy to Production
