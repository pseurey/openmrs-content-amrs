# PEP encounter form v1.0 — incomplete draft

The merged JSON is deliberately outside `configuration/` and unpublished. It is not ready to import. No concepts or encounter types were created or changed; the two supplied source forms are unchanged.

## Applied

- Retained one copy of visit date, provider, facility, occupation, exposure/reporting timestamps, time since exposure, source HIV status, recommendations, rapid HIV result, referrals and return date.
- Used datetime controls for exposure and reporting timestamps.
- Removed the initial and follow-up fields marked Remove, including the duplicate follow-up exposure date, ARV history, hepatitis fields, violence questions, excluded laboratory results, PHDP and assessment notes.
- Renamed Sexual Contact to Sexual exposure and used the existing Without condom and Sexual assault/rape answer concepts for Unprotected sex and Sexual assault.
- Retained percutaneous choices and conditional Other details.
- Added the repository's existing order-basket launcher pattern for prescriptions.
- Retained follow-up referrals despite their removal from the initial form; removed the TB/DOT program option. Fixed Other referral visibility to handle a multiselect value.

## Required before completion

| Requirement | Missing information / unresolved mapping |
| --- | --- |
| PEP follow-up encounter type | Neither source JSON has `encounterType` or `encounter`. The encounter type CSV has no PEP follow-up entry. Supply its existing UUID. |
| Method of exposure | Supply existing Sexual exposure and Non-occupational exposure answer UUIDs. Occupational exposure exists as `803b8da3-b200-4a6c-a682-979fd6478611`. The draft temporarily retains the original method choices rather than recoding Other or intercourse as different concepts. |
| Percutaneous occupation validation | Specify which occupations should enable percutaneous exposure for occupational cases. Non-occupational cases must also show percutaneous and body-fluid fields once their method concept is available. No occupation restriction is guessed in the draft. |
| Mucous membrane exposure | The source question `c0cbcbe6-2756-4134-b71a-d5763a2f0a4b` incorrectly offers only Blood. Supply existing answer UUIDs for Sexual contact, Eye/nose contact and Non-intact skin/percutaneous injury. This unresolved question is omitted from the draft. |
| Type of body fluid | Confirm the existing general body-fluid question UUID; the supplied `f10e249e-2061-43e8-ba9c-fa1eb64528e7` is labelled Other body fluids with visible blood. Supply missing answer UUIDs for CSF, semen, synovial fluid, blood culture, vaginal secretions, blood-stained fluids, pericardial fluid and HIV cultures. Blood, saliva, amniotic fluid, urine and pleural fluid UUIDs exist in the source. This unresolved question is omitted from the draft. |
| PEP outcome | The source Discharged question is `678bff8f-694d-42cc-9f70-b10e15daca9f` with Yes/No answers. Confirm whether it is the intended existing outcome concept, and supply the existing Not completed answer UUID. Completed exists as `a89c1ef8-1350-11df-a1f1-0026b9348838`. No Yes/No answers have been relabelled as completion outcomes. The outcome dropdown is omitted pending mapping. |
| Reasons for not completing PEP | Supply the existing question and Self-discontinuation answer UUIDs. Existing candidates include Patient stopped due to side effects (`a890d1ba-1350-11df-a1f1-0026b9348838`), Lost/ran out of pills (`a8af4cee-1350-11df-a1f1-0026b9348838`) and Forgot (`a89eacc2-1350-11df-a1f1-0026b9348838`). Confirm these candidates for this question. The field is omitted pending mapping and should display only for Not completed. |
| Violence screening link | Both tables remove all five screening questions but request linking after a Yes response. Specify where that response comes from after removal, and provide the existing violence screening form identifier. No target or trigger is fabricated. |

Once resolved, finish the conditional rules, assign the verified encounter type, validate in the form engine, and move the completed JSON into `configuration/backend_configuration/ampathforms/`.
