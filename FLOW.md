# Owner workflow and data flow

1. The owner creates a Google Cloud project and enables YouTube Data and
   Analytics APIs.
2. The owner reviews this documentation and grants upload/read access through
   Google's OAuth screen, selecting the MadewithLove channel. The setup script
   refuses to save a token for another channel.
3. The token is stored in the private GitHub repository's encrypted Actions
   secret. Source control contains no token.
4. A remote runner verifies channel access, restores the private checkpoint,
   checks tracked videos, and refreshes aggregate reports.
5. The runner chooses a creative variant, renders an original animation, and
   records its locally generated time slot before attempting upload.
6. Upload requires explicit enabled/public-verification settings. An uncertain
   or restricted upload stops subsequent uploads until manual reconciliation.
7. The runner saves API state in a private artifact with one-day retention,
   deletes superseded artifacts, and commits only local slot IDs.
8. The owner can pause, revoke Google consent, or invoke delete_data to remove
   stored worker API data. These operations do not delete YouTube videos.

Only the channel owner and authorized repository administrators can access the
private worker. No demo credentials granting access to the owner's accounts
are provided to third parties. Review access should be arranged separately.

Evidence: cloud validation succeeded for the original renderer, analytics
access, and four tests. The updated storage and selection behavior passes
nine local tests and must be validated on the remote runner before enabling.
