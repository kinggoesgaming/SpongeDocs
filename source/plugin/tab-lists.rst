=========
Tab Lists
=========

Tab lists are used in Minecraft to display the list of players currently on a server. The SpongeAPI allows for
manipulation of the tab list on a per-player basis.

To get a player's ``TabList``, you simply need to call the ``getTabList()`` method off of the ``Player`` who's
``TabList`` you wish to modify:

.. code-block:: java
    
    import org.spongepowered.api.entity.living.player.Player;
    import org.spongepowered.api.entity.living.player.tab.TabList;
    
    TabList tablist = player.getTabList();

Now that we have obtained the ``TabList``, we can modify several components of it. For example, to set the header and
footer of the ``TabList``, we simply need to call their appropriate methods:

.. code-block:: java
    
    import org.spongepowered.api.text.Text;
    import org.spongepowered.api.text.format.TextColors;
    
    tablist.setHeader(Text.of(TextColors.GOLD, "The tab list header"));
    tablist.setFooter(Text.of(TextColors.RED, "The tab list footer"));

Or we can call the ``setHeaderAndFooter()`` method:

.. code-block:: java
    
    tablist.setHeaderAndFooter(Text.of("header"), Text.of("footer"));

Tab List Entries
================

Now that we have set the header and footer of the ``TabList``, we can also add our own entries to the list. An example
of this is shown below:

.. code-block:: java
    
    import org.spongepowered.api.entity.living.player.gamemode.GameModes;
    import org.spongepowered.api.entity.living.player.tab.TabListEntry;
    import org.spongepowered.api.profile.GameProfile;
    
    TabListEntry entry = TabListEntry.builder()
        .list(tablist)
        .gameMode(GameModes.SURVIVAL)
        .profile(gameProfile)
        .build();
    tablist.addEntry(entry);

Now let's break this down. We set the ``TabListEntry`` to our specified ``TabList`` using the ``list()`` method. We
then set the game mode of our entry to ``SURVIVAL``. We then need to specify the ``GameProfile`` that the entry is
associated with. This can either be constructed using the ``GameProfile.of()`` method or retrieved through other means.
To apply the entry to the tab list, we simply need to call the ``addEntry()`` method off of our ``TabList``.

We can flesh out our basic example by specifying things such as the display name or latency of the entry:

.. code-block:: java
    
    TabListEntry entry = TabListEntry.builder()
        .list(tablist)
        .displayName(Text.of("Spongie"))
        .latency(0)
        .profile(gameProfile)
        .build();
    tablist.addEntry(entry);

Here, we set the display name that our entry will appear under to `Spongie` using the ``displayName()`` method. We then
set the latency for our ``TabListEntry`` to five bars. See the ``TabListEntry#setLatency()`` method for more
information on how to specify other types of bars for our entry.
