# DevSecOps Security Scanning Strategy

## Overview

This document describes the philosophy and policies for security scanning implemented in this repository.

## Trivy File System Scan

### Core Philosophy

1. **Continuous Security Monitoring**
   - Regularly scan the entire repository file system to detect vulnerabilities in dependencies and configuration files
   - Support on-demand scanning through manual execution (workflow_dispatch) when needed

2. **Severity-Based Graduated Response**
   - **Critical Vulnerabilities**: Immediately fail the CI/CD pipeline and enforce remediation
   - **High Vulnerabilities**: Report as warnings but allow builds to continue (enabling phased remediation)

3. **Visualization and Tracking**
   - Record scan results in a Notion database to enable time-series tracking
   - Store detailed vulnerability information in toggle block format for each scan result

4. **Detailed Reporting**
   - Record information for each vulnerability including package name, vulnerability ID, current version, and fixable version
   - Group vulnerabilities by file to support efficient remediation efforts

### Implementation Details

#### Scan Configuration

- **Scan Target**: Repository root directory (`.`)
- **Detection Target**: Only Critical and High severity vulnerabilities
- **Unfixed Vulnerabilities**: Exclude vulnerabilities without available patches using `ignore-unfixed: true`
- **Output Format**: Save results in JSON format for subsequent processing

#### Result Processing Flow

1. **Aggregation**: Aggregate counts of Critical and High vulnerabilities using jq
2. **Notion Submission**:
   - Record scan ID, repository name, status, timestamp, and vulnerability counts
   - Store vulnerabilities per file in toggle block format (up to 100 items maximum)
3. **CI/CD Decision**: Fail the workflow if any Critical vulnerabilities are detected

### Security Policy

- **Critical Vulnerabilities**: Zero-tolerance policy. Immediate remediation required upon detection
- **High Vulnerabilities**: Recorded as warnings with recommended planned remediation. However, they do not block builds

### Operational Considerations

- Scans are primarily executed manually, but can be changed to scheduled execution or PR triggers as needed
- Notion recording enables tracking vulnerability trends and visualizing security improvement progress
- Notion submissions are limited to a maximum of 100 items even when large numbers of vulnerabilities are detected (performance consideration)
