# Rex Orange County — Campaign Decks

Private deck hosting for OOO x Rex Orange County.

- **Live site:** https://roc.ooo.io (password-protected)
- **Decks:** [`decks/`](decks/) — each deck is stored and served as a [StatiCrypt](https://github.com/robinmoisson/staticrypt) AES-256-encrypted HTML page. The password decrypts it in the browser. No plaintext content lives in this repo (it is public, as required for GitHub Pages on the free plan).
- `index.html` is the encrypted current deck, served at the site root.
- Search engines are blocked via `robots.txt` (`Disallow: /`) and a `noindex, nofollow, noarchive` meta tag.

## Updating the deck

1. Encrypt the new source file (keep originals off this repo — it's public):
   ```sh
   npx staticrypt "<source-file>.html" -p "<password>" -d /tmp/enc \
     -t gate-template.html \
     --template-title "OOO x Rex Orange County" \
     --template-placeholder "Password" --template-button "Enter" \
     --template-error "Wrong password, try again." --remember 14 --short
   mv /tmp/enc/<file>.html index.html
   ```
2. `gate-template.html` already includes the noindex meta tag and the OOO-styled layout (wordmark, logo, table row). Edit it to change the gate's look or copy.
3. Copy the encrypted file into `decks/` as well if it should be reachable at its own URL.
4. Commit and push — GitHub Actions deploys automatically.

## Changing the password

Re-run the `npx staticrypt` command above with a new `-p` value and push.
