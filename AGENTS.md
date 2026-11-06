<!-- LOVABLE:BEGIN -->
> [!IMPORTANT]
> This project is connected to [Lovable](https://lovable.dev). Avoid rewriting
> published git history — force pushing, or rebasing/amending/squashing commits
> that are already pushed — as it rewrites history on Lovable's side and the
> user will likely lose their project history.
>
> Commits you push to the connected branch sync back to Lovable and show up in
> the editor, so keep the branch in a working state.
<!-- LOVABLE:END -->

- Google OAuth returns to the public `/auth/callback` page, which confirms the session before opening `/admin`; this avoids transient missing-session redirects.
- Defer auth API calls from `onAuthStateChange` callbacks until the session lock is released to prevent sign-in deadlocks.
- Drive imports call the connector gateway (`https://connector-gateway.lovable.dev/google_drive/...`) from `requireSupabaseAuth`-guarded server functions after an in-handler admin role check, streaming `alt=media` downloads straight into the `midia` bucket via Storage REST (`duplex: "half"`); never buffer a whole Drive file in memory and never call the gateway from browser code.
