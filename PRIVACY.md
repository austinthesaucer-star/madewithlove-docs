# Privacy notice

Effective October 2, 2026. Operator: Jordan Canevari.
Contact: austinthesaucer@gmail.com.

MadewithLove Automation is a private tool for its owner's MadewithLove channel.
It uses YouTube API Services. See [Google's Privacy Policy](https://policies.google.com/privacy)
and [YouTube's Terms of Service](https://www.youtube.com/t/terms).

## Data and purpose

With the channel owner's consent, the tool verifies channel identity, uploads
original videos, and reads aggregate per-video analytics: engaged views,
average percentage viewed, watch time, and subscribers gained. It uses
YouTube's reported engaged views directly when choosing creative variants.
It does not request individual viewer records, audience demographics, revenue,
location, advertising identifiers, or contact lists. It has no advertising or
tracking SDKs and does not sell data.

## Storage and providers

Google processes OAuth authorization, video uploads, and analytics requests.
GitHub hosts the private source repository and executes the worker. The
Google OAuth token is held in an encrypted GitHub repository secret, with a
private local setup copy. API video IDs and aggregate analytics are held in a
private Actions state artifact with a one-day retention setting. Each
successful checkpoint replaces the previous one, which the worker requests
GitHub to delete. Locally generated slot IDs are retained in Git history to
avoid duplicate uploads; they contain no API video IDs or analytics.

Historical analytics cover the three complete calendar days after each video's
publication. The worker refreshes those reports and checks the continued
availability of tracked videos on each live run. Data for unavailable videos
is removed from the next checkpoint. API state is not committed to Git.
Provider-managed backups and deletion processing are subject to the providers'
practices. The runner's temporary workspace exists only for its job.

## Control, revocation, and deletion

The owner can pause uploads by clearing CHANNEL_ENABLED in repository variables.
Google authorization can be revoked at
[Google's permission settings](https://security.google.com/settings/security/permissions).
If the worker cannot refresh authorization or no longer matches the channel,
it clears API fields and requests deletion of its stored state artifacts.
Artifacts also expire under their one-day retention setting if runs stop.

The owner can invoke the Channel worker workflow with delete_data checked to
request immediate deletion of all worker state artifacts. Disable publishing
before invoking deletion. For help or deletion of local setup copies, contact
austinthesaucer@gmail.com; requests will be handled within seven calendar days.
GitHub repository administrators control the OAuth secret and can remove it.

Deleting worker data does not delete YouTube videos or other data held by
YouTube. Manage those separately through YouTube Studio. A missing checkpoint
stops publishing until reconciliation, rather than risking duplicate uploads.

## Status

This notice describes the updated implementation. Public publishing is disabled
while setup, remote verification, and YouTube's API audit are completed.
