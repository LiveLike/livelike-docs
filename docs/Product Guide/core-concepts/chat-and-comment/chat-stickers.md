---
title: Chat stickers
deprecated: false
hidden: false
metadata:
  robots: index
---
Stickers bring personality and fun into chat conversations. They’re more than just images — they’re interactive, expressive, and can be tailored to your community or brand.
Inside the LiveLike chat, users can send stickers just like emojis, but with far more creative flexibility: animated reactions, team logos, brand partnerships, or even exclusive packs for VIP users.

By using stickers, you can:

* Enrich conversations with creative, on-brand visuals
* Unlock sponsorship and partnership opportunities
* Reward and recognize your most engaged users
* Offer fans new ways to express themselves during live or on-demand content

***

### Sticker Packs

Stickers are grouped into packs that share a theme or art style. Packs can be based on:

* Players and Teams
* Leagues and Tournaments
* Crowd Reactions (cheers, boos, celebrations)
* Personalities or Influencers

<Image align="center" alt={563} border={false} caption="Each pack has its own icon, making it easy for users to find in their chat keyboard." title="Sticker Keyboard Behavior" src="https://files.readme.io/5239f1d-sticker_kb_behavior.gif" width="auto" />

💡 **Flexible setup:** You can enable multiple packs across your app, and each chat can use a different combination of packs or share the same ones.
This means a “match-day chat” could feature team and league stickers, while a “fan community chat” might highlight personality-driven packs.

***

### Custom Stickers

Your team can create custom sticker packs to perfectly match your app’s identity.
For best results, follow the [Chat Asset Guidelines](doc:chat-sticker-guidelines) for size, file format, and styling. -- ---- edit link

Custom packs let you:

* Extend your brand identity inside chat
* Launch theme-based campaigns or seasonal sticker sets
* Create limited-time packs for special events

***

### Sponsorship Opportunities

Stickers can also serve as sponsored assets.
For example, a brand could provide a sticker pack that fans can use to cheer during a live event. This creates natural engagement while opening up new monetization opportunities.

LiveLike provides [analytics and reports](doc:analytics-overview) so you can track: ------ edit link

* How often sponsored stickers are used
* Which stickers are most popular
* User engagement trends during live moments

***

### Exclusive Sticker Packs ✨

Exclusive stickers unlock a new layer of personalization and recognition inside your community chats.
Unlike standard packs, exclusive packs are only available to specific users or groups — helping fans feel rewarded and distinguished, while also opening up new monetization and engagement opportunities.

<Callout icon="📘" theme="info">
  Exclusive packs are managed at the profile level. Only profiles that have been granted access will see and use them inside chat.
</Callout>

**Sample Use Cases**

* In-app purchases for fans who love collecting.
* Team-branded packs available only to official fan groups.
* Collectible packs redeemable in the Rewards Store.
* Gold-tier members unlocking exclusive packs as part of loyalty benefits.

**How It Works**

* Exclusive sticker packs are marked with an is_exclusive flag.
* Access can be granted, revoked, or automated through purchases, tier benefits, or quest rewards.
* Fans will only see packs they have access to, ensuring personalized chat experiences without clutter.

#### APIs – Integrator Experience

* Grant Access to a Sticker Pack
  `POST /api/v1/profiles/{profile_uuid}/sticker-packs/`
  Grants access to an exclusive sticker pack for the specified profile.
  ```Text Request Body
  { 
    "sticker_pack_id": "6e654321-abcd-4def-9012-9876543210fe", 
  }
  ```
* **List** All Sticker Packs Owned by Profile
  Retrieves a paginated list of all sticker packs currently owned by the specified profile.
  `GET /api/v1/profiles/{profile_uuid}/sticker-packs/`
* **Revoke** Access to a Sticker Pack

  Revokes the user’s access to a specific sticker pack.

  `DELETE /api/v1/profiles/{profile_uuid}/sticker-packs/{sticker_pack_id}/`
* Sticker Pack Create/Update APIs
  **Update** existing APIs to enable integrators to control the value of the `is_exclusive` field.
* Usage APIs
  **Modify** the ChatRoom sticker pack API:
  `GET /api/v1/chat-rooms/{chat-room-id}/sticker-packs/`
  Ensure users see and use exclusive sticker packs (along with common ones) only if they have access.
  ```
  stickers = chat_room.sticker_packs.filter(
  Q(is_exclusive=False) | Q(is_exclusive=True, profile_sticker_packs__profile=profile)
  )
  ```

**To support exclusive ownership of sticker packs by fans, we’ll enhance the data model in two ways:**

1. Add is_exclusive Field to StickerPack Model
   This field distinguishes exclusive packs from public ones.
   ```
   class StickerPack(UUIDModel):
       ...
       is_exclusive = models.BooleanField(default=False)
   ```
2. Add ProfileStickerPack Model
   This new model tracks which profile owns which sticker pack. Multiple users can own the same exclusive pack (e.g., via purchase).
   ```
   class ProfileStickerPack(models.Model):
       profile = models.ForeignKey(
           ApplicationProfile, related_name="profile_sticker_packs", on_delete=models.CASCADE
       )
       sticker_pack = models.ForeignKey(
           StickerPack, related_name="profile_sticker_packs", on_delete=models.CASCADE
       )
       created_at = models.DateTimeField(auto_now_add=True)
       removed_at = models.DateTimeField(null=True, blank=True)

       class Meta:
           ordering = ("pk",)
           constraints = [
               models.UniqueConstraint(
                   fields=("profile", "sticker_pack"),
                   condition=Q(removed_at__isnull=True),
                   name="uniq_profile_stickerpack",
               ),
           ]
   ```
