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
