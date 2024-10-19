# Utilizing OWASP Dependency Check within the Services Standard Build (SSB)

## Utilizing OWASP Dependency Check within the Services Standard Build (SSB)

The sources emphasize the importance of security in IdentityIQ deployments and highlight the integration of the OWASP Dependency Check utility within the SSB to address potential vulnerabilities stemming from third-party libraries.

### OWASP Dependency Check: A Security Essential

The Open Web Application Security Project (OWASP) offers a valuable tool known as Dependency Check, designed to scan project dependencies for known vulnerabilities. This utility is incorporated into the SSB, enabling it to assess third-party libraries bundled with IdentityIQ or introduced by implementers for any publicly disclosed security flaws.

### Vulnerability Detection and Reporting

When executed, the Dependency Check utility meticulously analyzes library files situated in the `build/extract/WEB-INF/lib` and `build/extract/WEB-INF/lib-connectors` directories, comparing them against the National Vulnerability Database (NVD) maintained by NIST.  Upon completion, comprehensive reports detailing identified vulnerabilities are generated in the `build/dependency-check-reports` folder. These reports are available in various formats, including:

*   **HTML:** Offers a user-friendly, web-based report suitable for detailed analysis.
*   **CSV:**  Presents the findings in a comma-separated value format, ideal for spreadsheet software or data processing.
*   **XML:** Provides a structured, machine-readable report for further processing or integration into other systems.
*   **JSON:** Delivers the results in a JavaScript Object Notation format, commonly used for data exchange in web applications.

The reports furnish crucial information about each vulnerability, encompassing:

*   **CVE Number:** A unique identifier assigned to the vulnerability in the Common Vulnerabilities and Exposures (CVE) system.
*   **Description:** A concise explanation of the vulnerability and its potential impact.
*   **Severity Classification:** A rating indicating the severity of the vulnerability (e.g., Low, Medium, High, Critical).
*   **CVSS Score:** A numerical representation of the vulnerability's severity based on the Common Vulnerability Scoring System (CVSS).
*   **Affected Library:** The specific third-party library where the vulnerability is present.

### Running the Dependency Check Utility

Invoking the Dependency Check analysis within the SSB involves executing the `dependency-check` target. This can be achieved by running the command `build dependency-check` from a system with an active internet connection. The utility requires internet access to retrieve the most up-to-date vulnerability data from the NVD.

**Note:** Initial execution of the utility might take some time as it downloads the latest vulnerability dataset. Subsequent runs typically proceed faster as the data is cached locally.

### Managing False Positives and Suppressions

The Dependency Check utility might occasionally flag vulnerabilities that are not actual threats within the context of the IdentityIQ implementation—these are known as false positives. To prevent these false positives from cluttering the reports and obscuring genuine vulnerabilities, the SSB provides a mechanism to suppress specific CVE entries.

A sample `suppressions.xml` file is included in the `dependency-check-ant` directory at the root of the SSB. Within this file, developers can define `<suppress>` entries, specifying the CVE to be suppressed and optionally providing justifications for the suppression.

**Example:**

```xml
<suppress>
  <notes><![CDATA[
    This suppresses CVE-2017-5662 for batik-awt-util-1.6-1.jar.
    The documented CVE for this version of this library is related to an XML Entity Attack while parsing SVG files. 
    This attack vector is not applicable in our implementation.
  ]]></notes>
  <gav>batik:batik-awt-util:1.6-1</gav>
  <cve>CVE-2017-5662</cve>
</suppress>
```

### Updating the Dependency Check Utility

The OWASP Dependency Check utility is frequently updated to incorporate newly discovered vulnerabilities and enhance its analysis capabilities. To ensure the SSB utilizes the latest version, developers can download the updated utility from:

```
https://jeremylong.github.io/DependencyCheck/dependency-check-ant/index.html
```

After downloading the updated utility, replace the existing `dependency-check-ant` folder at the root of the SSB with the contents of the downloaded package. **Remember to preserve the customized `suppressions.xml` file by copying it to the new `dependency-check-ant` folder.**

### Addressing Exclusions

The Dependency Check utility, by default, excludes files containing the string "ojdbc." This exclusion is in place to accommodate Oracle's licensing restrictions, which prohibit the distribution of Oracle JDBC drivers through public repositories. Developers should always ensure they are utilizing the most recent version of the Oracle JDBC driver and remain mindful of Oracle's licensing terms.

### Importance of Dependency Check

Regularly employing the Dependency Check utility as part of the SSB workflow significantly bolsters the security posture of IdentityIQ deployments. By proactively identifying and mitigating vulnerabilities in third-party libraries, organizations can minimize the risk of exploitation and enhance the overall resilience of their IAM infrastructure.
