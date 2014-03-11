package io.github.Tudedude100;

import java.text.SimpleDateFormat;
import java.util.Arrays;
import java.util.Date;

import org.bukkit.OfflinePlayer;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerLoginEvent;
import org.bukkit.event.player.PlayerLoginEvent.Result;
import org.bukkit.plugin.PluginManager;
import org.bukkit.plugin.java.JavaPlugin;

public class GocadacraftBan extends JavaPlugin implements Listener{

//Made by Tudedude(Tudedude100) for DoctorGocada
//Using Bukkit for Craftbukkit servers
//Bukkit intellectual property of the Bukkit coding team
//I claim no rights to Bukkit, only the code of this project itself
//Dated 3/10/14 - 7:50 PM PST
	
	public void onEnable(){
		PluginManager pm = getServer().getPluginManager();
		pm.registerEvents(this, this);
		loadConfig();
	}
	
	public void loadConfig(){
		String path1 = "bans";
		String path2 = "banned";
		getConfig().addDefault(path1, "");
		getConfig().addDefault(path2, "");
		getConfig().options().copyDefaults(true);
		saveConfig();
	}
	
	@SuppressWarnings("deprecation")
	public boolean onCommand(CommandSender sender, Command cmd, String label, String[] args){
		if(cmd.getLabel().equalsIgnoreCase("ban")){
			if(sender.hasPermission("Gocadacraft.ban") || sender.isOp() || sender.hasPermission("*")){
				String path = "bans." + sender.getName();
				Date now = new Date();
				SimpleDateFormat format = new SimpleDateFormat("dd-MM-yyyy HH:mm:ss");
				if(args.length==1){
					if(getConfig().contains(path)){
						if(getServer().getPlayer(args[0]).isOnline()){
							Player tar = getServer().getPlayer(args[0]);
							tar.setBanned(true);
							String[] list = {sender.getName() + " banned " + tar.getName() + " on " + format.format(now) + " with no given reason."};
							getConfig().getStringList("banned").add(getServer().getPlayer(args[0]).getName());
							getConfig().getStringList(path).add(Arrays.asList(list));
						}else{
							OfflinePlayer tar = getServer().getOfflinePlayer(args[0]);
							tar.setBanned(true);
							String[] list = {sender.getName() + " banned " + tar.getName() + " on " + format.format(now) + " with no given reason."};
							getConfig().set(path, Arrays.asList(list));
						}
						return true;
					}else{
						if(getServer().getPlayer(args[0]).isOnline()){
							Player tar = getServer().getPlayer(args[0]);
							tar.setBanned(true);
							String[] list = {sender.getName() + " banned " + tar.getName() + " on " + format.format(now) + " with no given reason."};
							getConfig().getStringList("banned").add(getServer().getPlayer(args[0]).getName());
							getConfig().set(path, Arrays.asList(list));
						}else{
							OfflinePlayer tar = getServer().getOfflinePlayer(args[0]);
							tar.setBanned(true);
							String[] list = {sender.getName() + " banned " + tar.getName() + " on " + format.format(now) + " with no given reason."};
							getConfig().set(path, Arrays.asList(list));
						}
						return true;
					}
				}else if(args.length == 0){
					
					sender.sendMessage(" §7-§8x§7-§8x§7-§8x§7-§3Developed by Tudedude §7- §6§lGocadacraftBan§7-§8x§7-§8x§7-§8x§7-");
					sender.sendMessage("                                      §4§lCommands");
					sender.sendMessage("§2/ban <player> [reason] §3§l - §6Bans a player, optionally \n" +
									   "for a given reason.");
					sender.sendMessage("§2/tban <player> <time(hours)> [reason] §3§l- §6Temporarily\n" +
							           "bans a player, optionally for a given reason.");
					sender.sendMessage("§2/unban <player> or /pardon <player> §3§l- §6Removes a player's ban\n" +
							           "or tempban.");
					
				}
				return true;
			}else{
				sender.sendMessage("You don't have permission to execute this command.");
				return true;
			}
		}
		if(cmd.getLabel().equalsIgnoreCase("tban")){
			if(sender.hasPermission("Gocadacraft.ban") || sender.isOp() || sender.hasPermission("*")){
				String path = "bans." + sender.getName();
				Date now = new Date();
				SimpleDateFormat format = new SimpleDateFormat("dd-MM-yyyy HH:mm:ss");
				if(args.length==1){
					if(getConfig().contains(path)){
						getConfig().getStringList("path.to.list").add("A new string");
						return true;
					}else{
						Player tar = getServer().getPlayer(args[0]);
						if(tar == null){
							getServer().getOfflinePlayer(args[0]).setBanned(true);
						}
						String[] list = {sender.getName() + " banned " + tar.getName() + " on " + format.format(now) + " with no given reason."};
						getConfig().set("path.to.list", Arrays.asList(list));
						return true;
					}
				}else if(args.length == 0){
					
					sender.sendMessage(" §7-§8x§7-§8x§7-§8x§7-§3Developed by Tudedude §7- §6§lGocadacraftBan§7-§8x§7-§8x§7-§8x§7-");
					sender.sendMessage("                                      §4§lCommands");
					sender.sendMessage("§2/ban <player> [reason] §3§l - §6Bans a player, optionally \n" +
									   "for a given reason.");
					sender.sendMessage("§2/tban <player> <time(hours)> [reason] §3§l- §6Temporarily\n" +
							           "bans a player, optionally for a given reason.");
					sender.sendMessage("§2/unban <player> or /pardon <player> §3§l- §6Removes a player's ban\n" +
							           "or tempban.");
					
				}
				return true;
			}else{
				sender.sendMessage("§cYou don't have permission to execute this command.");
				return true;
			}
		}
		if(cmd.getLabel().equalsIgnoreCase("unban") || cmd.getLabel().equalsIgnoreCase("pardon")){
			if(sender.hasPermission("Gocadacraft.ban") || sender.isOp() || sender.hasPermission("*")){
				if(args.length==1){
					OfflinePlayer tar = getServer().getOfflinePlayer(args[0]);
					if(tar.isBanned()){
						tar.setBanned(false);
					}else{
						
					}
				}else{
					sender.sendMessage(" §7-§8x§7-§8x§7-§8x§7-§3Developed by Tudedude §7- §6§lGocadacraftBan§7-§8x§7-§8x§7-§8x§7-");
					sender.sendMessage("                                      §4§lCommands");
					sender.sendMessage("§2/ban <player> [reason] §3§l - §6Bans a player, optionally " +
									   "for a given reason.");
					sender.sendMessage("§2/tban <player> <time(hours)> [reason] §3§l- §6Temporarily " +
							           "bans a player, optionally for a given reason.");
					sender.sendMessage("§2/unban <player> or /pardon <player> §3§l- §6Removes a player's ban" +
							           " or tempban.");
				}
			}else{
				sender.sendMessage("§cYou don't have permission to execute this command.");
			}
		}
		return false;
	}
	
	@EventHandler
	public void onPlayerLogin(PlayerLoginEvent e){
		
		if(e.getResult() == Result.KICK_BANNED){
			String kickMsg = getConfig().getString("banned." + e.getPlayer().getName()+".reason");
			e.setKickMessage(kickMsg);
		}
		
	}

}

Plugin.yml
==========

name: GocadacraftBan
main: io.github.Tudedude100.GocadacraftBan
version: 0.01
commands:
  ban:
    description: Bans target player, optionally with a reason.
    usage: /ban <player> [reason]
  tban:
    description: Temporarily bans target player, optionally with a reason.
    usage: /tban <player> <time(hours)> [reason]
  unban:
    description: Pardons target player from a ban, temporary or permanent.
    usage: /unban <player>
  pardon:
    description: Pardons target player from a ban, temporary or permanent.
    usage: /pardon <player>
