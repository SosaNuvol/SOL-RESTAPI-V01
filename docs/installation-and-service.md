# Installation topology and field experience

## What an installer opens

Customer → property → installed system → current approved topology. Show property address, system status, commissioning date, warranty assessment, component list, and the most recent completed service summary. Clearly show the revision number and when the device last synchronized.

Offer diagram and list views. Filter by controller, Y splitter, power booster, signal booster, and light segment. Selecting a component reveals its location description, context/close-up photos, connected ports and cables, identification, access instructions, and repair history.

Example location: “North-facing rear roofline, behind the gutter at the northwest corner, approximately two feet east of the downspout. Accessible from the rear patio.” A street address or GPS point alone cannot locate a roofline splitter.

Use stable component labels such as Y-01 and PB-02, optionally with QR labels. Diagram coordinates are drawing positions, not physical coordinates. Store actual location separately and support photo/facade image anchors. A Y splitter is one asset with named ports and explicit connections, not merely a freehand symbol.

## Initial installation

1. Download the assigned job and necessary customer/property details before travel.
2. Record installed products, quantities, serials where relevant, and installers' labor.
3. Place each serviceable component, describe its location, and add context and close-up photos.
4. Connect ports to capture actual cable routes, light segments, controller, splitters, and boosters. Record power supply/circuit information where useful for troubleshooting.
5. Verify operation, record commissioning measurements/checklist and customer handoff.
6. Submit the draft. Publication validates material/asset consistency, topology, required evidence, and completion checks. The approving role can be the lead installer or office reviewer, as agreed.

## Warranty repair

1. Office logs symptoms and selects the correct property/system. Record a warranty assessment instead of assuming every failure within a date window is covered.
2. Installer opens the approved topology and identifies the suspected component using descriptions/photos.
3. Record observed symptoms, diagnostic steps, failed asset, likely cause, and before photos.
4. Record removed/replacement products, quantities and actual cost; track installer compensation even when the customer owes nothing.
5. Fork a draft topology from the current revision if anything changes. Preserve stable asset IDs for unchanged components and create new assets for replacements.
6. Add after photos of changed locations and connections, a description of the fix, and test results.
7. Upload evidence, validate, approve the revision, and close the job. A repair without a layout change still adds a repair record and evidence.

Do not close a job as fully documented while required images remain only on a device. Allow a visible “work complete, documentation pending sync” state so physical completion is distinguishable from reviewed records.

## Revision behavior

Example: Revision 1 places Y-01 at the rear northwest gutter. A service visit relocates it into an accessible enclosure and replaces PB-02. Revision 2 records the new location, new booster asset, connections, and photos. Revision 1 remains available with the service work order explaining the change.

If another installer publishes a revision while a device is offline, reject automatic publication of the stale draft. Show the difference and require reconciliation against the current revision. Never overwrite the whole topology with last-write-wins.

## Offline and attachments

Cache only assigned jobs and explicitly downloaded history in device SQLite. Cache component photos separately with storage limits. If evidence is not downloaded, show that clearly. Queue commands with client-generated IDs; retrying a command must not create another repair or payment entry.

Each command carries the base row/revision version. Server validation returns accepted, rejected, or conflict status. Append-only observations may merge; changed assignments, topology, amounts, and status transitions require concurrency handling. Sync deletion tombstones and authorization revocations when online. Set an offline-access expiration policy and clear cached records on logout where supported.

Use resumable photo uploads, checksums, and explicit pending/ready/failed states. Keep the original plus derived thumbnails/annotations. Store captured time separately from uploaded time. Protect cached data using platform secure storage/encryption where supported and account for lost devices. Mobile synchronization is a significant feature with its own pilot and failure testing.

## Initial screens

ERP: lead pipeline, customer account, property/system record, quote/order, installation schedule, topology viewer/editor, service queue, staff attribution/compensation, costs and reports, integration exception queue.

Installer mobile: assigned jobs, offline download status, component finder, camera/location capture, material/labor entries, diagnostics, revision submission, personal completion/payment history when authorized.

Sales mobile: assigned leads, contact history, property survey/photos, quote/order status, representative attribution, follow-ups, and authorized commission status. Share libraries between mobile apps while keeping the workflows focused.
