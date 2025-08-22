# Ketryx Demo
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fwilliam-ketryx%2Fstandard-demo.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Fwilliam-ketryx%2Fstandard-demo?ref=badge_shield)


This is a sample repository highlighting the [Ketryx Platform](https://www.ketryx.com/platform) features around [Git-based configuration items](https://docs.ketryx.com/manuals/man-09-git-based-configuration-items) and [automated test reporting](https://docs.ketryx.com/manuals/man-06-test-management#id-3.-automated-tests).

## Structure

* A [Java function](java-src/src/main/java/com/ketryx/sample/SensorReading.java) annotated with a specification and corresponding [JUnit test](java-src/src/test/java/com/ketryx/sample/SensorReadingTest.java).
* A [Markdown specification](markdown/spec-sensor-module.md) tested by a [Markdown test case](markdown/test-sensor-module.md) that is executed by a [Jest test](js-src/tests/testSensorModule.ts).
* A [Javascript function](js-src/app/createSensorWarning.ts) annotated with a specification that is tested by a [Cucumber test](js-src/features/sensor-module.feature).

Automated tests are executed and reported to Ketryx as part of the [CI/CD GitHub Actions workflow](.github/workflows/cicd.yml), with steps like the following:

```yaml
  - name: Report JS build to Ketryx
    uses: Ketryx/ketryx-github-action@v1
    if: success() || failure()
    with:
      ketryx-url: ${{ vars.KETRYX_URL }}
      project: ${{ vars.KETRYX_PROJECT }}
      version: ${{ vars.KETRYX_VERSION }}
      api-key: ${{ secrets.KETRYX_API_KEY }}
      build-name: ci-js
      test-junit-path: test-results/jest-junit.xml
      test-cucumber-path: test-results/cucumber-report.json

  - name: Report Java build to Ketryx
    uses: Ketryx/ketryx-github-action@v1
    if: success() || failure()
    with:
      ketryx-url: ${{ vars.KETRYX_URL }}
      project: ${{ vars.KETRYX_PROJECT }}
      version: ${{ vars.KETRYX_VERSION }}
      api-key: ${{ secrets.KETRYX_API_KEY }}
      build-name: ci-java
      test-junit-path: java-src/build/test-results/test/*.xml
```

## Install dependencies

```bash
npm install
```

## Running Tests

Run unit and integration tests:

```bash
npm run test:unit-integration-ci
```

Run tests in watch mode:

```bash
npm test
```

Run end-to-end tests:

```bash
npm run test:e2e
```

Run Java unit tests:

```bash
cd java-src
./gradlew test
```


## License
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Fwilliam-ketryx%2Fstandard-demo.svg?type=large)](https://app.fossa.com/projects/git%2Bgithub.com%2Fwilliam-ketryx%2Fstandard-demo?ref=badge_large)