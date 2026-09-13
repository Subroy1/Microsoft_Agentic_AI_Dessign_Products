# AutoGen Agent Topology

This topology reflects the orchestration implemented in [code.py](code.py): a `GroupChat` with a `GroupChatManager` and four cooperating agents.

```mermaid
flowchart TD
    U[UserProxy\nHuman / Workflow Trigger]
    M[GroupChatManager\nOrchestrator]
    D[DocumentScanner\nStep 1: scan & categorize]
    C[ComplianceChecker\nStep 2: detect compliance issues]
    R[ReviewCoordinator\nStep 3: route & assign actions]
    L[Legal / Executive Review\nCritical escalations]
    P[Department Head\nMajor issues]
    O[Document Owner\nMinor revisions]

    U -->|1. Start compliance batch| M
    M -->|2. Broadcast task| D
    D -->|3. Extract metadata + classify docs| C
    C -->|4. Flag issues + severity| R
    R -->|5. Route decision| L
    R -->|6. Approval path| P
    R -->|7. Revision request| O
    L -->|8. Final legal review| U
    P -->|9. Department approval| U
    O -->|10. Corrective update| U

    subgraph Workflow
        D
        C
        R
    end
```

## Orchestration flow

1. `UserProxy` starts a batch workflow with the sample documents.
2. `GroupChatManager` coordinates the conversation between agents.
3. `DocumentScanner` inspects each document, derives metadata, and identifies document type.
4. `ComplianceChecker` reviews for missing approvals, outdated references, or incomplete sections.
5. `ReviewCoordinator` assigns issue severity and decides routing.
6. `Legal/Executive`, department heads, or document owners handle the resolution path depending on the issue class.

## Labels used in the code

- `DocumentScanner` = document intake and categorization
- `ComplianceChecker` = issue detection and severity classification
- `ReviewCoordinator` = routing, remediation planning, and audit trail
- `UserProxy` = human-triggered workflow initiator
- `GroupChatManager` = orchestration engine for the multi-agent runtime
