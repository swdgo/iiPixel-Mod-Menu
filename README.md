using System.Numerics;
using System.Xml.Linq;
using static System.Net.Mime.MediaTypeNames;
using static System.Runtime.CompilerServices.RuntimeHelpers;

< Window x: Class = "iiPixelsModMenu.MainWindow"
        xmlns = "http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns: x = "http://schemas.microsoft.com/winfx/2006/xaml"
        Title = "Mod Menu" Height = "300" Width = "400" Loaded = "MainWindow_Loaded" >
    < Grid >
        < ListBox Name = "ModList" HorizontalAlignment = "Left" Height = "200" Margin = "10,10,0,0" VerticalAlignment = "Top" Width = "120" SelectionChanged = "ModList_SelectionChanged" />
        < Button Content = "Apply" HorizontalAlignment = "Left" Margin = "150,10,0,0" VerticalAlignment = "Top" Width = "75" Click = "ApplyButton_Click" />
        < Button Content = "Close" HorizontalAlignment = "Left" Margin = "250,10,0,0" VerticalAlignment = "Top" Width = "75" Click = "CloseButton_Click" />
    </ Grid >
</ Window >

using System.Collections.Generic;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Input;

namespace iiPixelsModMenu
{
    public partial class MainWindow : Window
    {
        private List<string> availableMods = new List<string>
        {
            "Bee All",public static void BetterBeeAll()
        {
            if (PhotonNetwork.IsMasterClient == true)
            {
                if (ControllerInputPoller.instance.rightControllerPrimaryButton)
                {
                    foreach (Player p in PhotonNetwork.PlayerListOthers)
                    {
                        VRRig rig = GorillaGameManager.instance.FindPlayerVRRig(p);
                        AngryBeeSwarm.instance.Emerge(rig.rightHandTransform.position, rig.transform.position);
                        AngryBeeSwarm.instance.targetPlayer = p;
                        AngryBeeSwarm.instance.grabbedPlayer = p;
                    }
                }
            }
            else
            {
                if (ControllerInputPoller.instance.rightControllerPrimaryButton)
                {
                    NotifiLib.SendNotification("<color=red> ERROR </color> <color=purple> YOU ARE NOT </color> <color=yellow> MASTER CLIENT </color>");
                }
            }
        }
            "Fly",using UnityEngine;

public class FlyScript : MonoBehaviour
    {
        public float flySpeed = 10f;
        public float gravity = 9.81f;

        private CharacterController characterController;
        private bool isFlying = false;

        void Start()
        {
            characterController = GetComponent<CharacterController>();
        }

        void Update()
        {
            if (Input.GetKeyDown(KeyCode.X))
            {
                isFlying = !isFlying; 
            }

            if (isFlying)
            {
                
                Vector3 moveDirection = transform.forward * Input.GetAxis("Vertical") +
                                        transform.right * Input.GetAxis("Horizontal");

                
                moveDirection = moveDirection.normalized * flySpeed * Time.deltaTime;

                
                moveDirection.y -= gravity * Time.deltaTime;

                
                characterController.Move(moveDirection);
            }
        }
    }

            "FingerPainterDetector",public static void FingerPainterDetector()
        {
            foreach (VRRig vrrig in GorillaParent.instance.vrrigs)
            {
                if (!vrrig.isOfflineVRRig && vrrig.concatStringOfCosmeticsAllowed.Contains("LBADE"))
                {
                    NotifiLib.SendNotification("<color=yellow> INFO </color> <color=cyan> FINGER PAINTER DETECTED IN LOBBY! </color>");
                }
            }
        }
        "StickDetector",public static void ModeratorDetector()
        {
            foreach (VRRig vrrig in GorillaParent.instance.vrrigs)
            {
                if (!vrrig.isOfflineVRRig && vrrig.concatStringOfCosmeticsAllowed.Contains("LBAAK"))
                {
        "LemmingDetector",public static void AdminBadgeDetector()
                {
                    foreach (VRRig vrrig in GorillaParent.instance.vrrigs)
                    {
                        if (!vrrig.isOfflineVRRig && vrrig.concatStringOfCosmeticsAllowed.Contains("ADMINISTRATOR BADGE"))
                        {
                            "Disconnect",public static void DisconnectButton()
        {
            if (ControllerInputPoller.instance.rightControllerPrimaryButton)
            {
                if (PhotonNetwork.InRoom == true)
                {
                    PhotonNetwork.Disconnect();
                    NotifiLib.SendNotification("<color=yellow> INFO </color> <color=cyan> Succesfully Disconnected! </color>");
                }
                else
                {
                    NotifiLib.SendNotification("<color=yellow> INFO </color> <color=cyan> YOU ARE NOT CONNECTED TO A ROOM </color>");
                }
            }
        }
        "Anti-Ban",public static void FlushRPCs()
        {
            if (ControllerInputPoller.instance.rightControllerPrimaryButton)
            {
                GorillaNot.instance.rpcCallLimit = int.MaxValue;
                PhotonNetwork.RemoveRPCs(PhotonNetwork.LocalPlayer);
                PhotonNetwork.OpCleanActorRpcBuffer(PhotonNetwork.LocalPlayer.ActorNumber);
                PhotonNetwork.OpCleanRpcBuffer(GorillaTagger.Instance.myVRRig);
                PhotonNetwork.RemoveBufferedRPCs(GorillaTagger.Instance.myVRRig.ViewID, null, null);
                NotifiLib.SendNotification("<color=yellow> INFO </color> <color=cyan> Succesfully Flushed RPCs! </color>");
            }
        }
        "Speed-Boost",public static void Mosaboost()
        {
            GorillaLocomotion.Player.Instance.maxJumpSpeed = 7f;
            GorillaLocomotion.Player.Instance.jumpMultiplier = 7;
        }
        "Anti-Report",public static void AntiReport()
        {
            try
            {
                GameObject gameObject = GameObject.Find("Environment Objects/PersistentObjects_Prefab/GorillaUI");
                Transform transform = gameObject.transform;
                for (int i = 0; i < transform.childCount; i++)
                {
                    Transform transform2 = transform.GetChild(i);
                    bool flag = transform2.gameObject.name.Contains("Anchor") && transform2.gameObject.activeSelf;
                    if (flag)
                    {
                        transform2 = transform2.Find("GorillaScoreBoard(Clone)");
                        for (int j = 0; j < transform2.childCount; j++)
                        {
                            Transform child = transform2.GetChild(j);
                            bool flag2 = child.name.Contains("GorillaPlayerScoreboardLine");
                            if (flag2)
                            {
                                Text component = child.Find("Player Name").GetComponent<Text>();
                                Transform transform3 = child.Find("ReportButton");
                                bool flag3 = component != null;
                                if (flag3)
                                {
                                    bool flag4 = component.text == PhotonNetwork.LocalPlayer.NickName.ToUpper();
                                    if (flag4)
                                    {
                                        foreach (VRRig vrrig in GorillaParent.instance.vrrigs)
                                        {
                                            bool flag5 = vrrig != GorillaTagger.Instance.offlineVRRig;
                                            if (flag5)
                                            {
                                                float num = Vector3.Distance(vrrig.rightHandTransform.position, transform3.position);
                                                float num2 = Vector3.Distance(vrrig.leftHandTransform.position, transform3.position);
                                                bool flag6 = num < 1f || num2 < 1f;
                                                if (flag6)
                                                {
                                                    PhotonNetwork.Disconnect();
                                                    NotifiLib.SendNotification("<color=red> ANTIREPORT </color> <color=purple> Someone Tried To Report You! </color>");
                                                }
                                            }
                                        }
                                    }
                                }
                                else
                                {
                                    UnityEngine.Debug.LogError("Odd error, no name");
                                }
                            }
                        }
                    }
                }
            }
            catch
            {
            }
        }
        "NoFingerMovement",public static void NoFinger()
        {
            ControllerInputPoller.instance.leftControllerGripFloat = 0f;
            ControllerInputPoller.instance.rightControllerGripFloat = 0f;
            ControllerInputPoller.instance.leftControllerIndexFloat = 0f;
            ControllerInputPoller.instance.rightControllerIndexFloat = 0f;
            ControllerInputPoller.instance.leftControllerPrimaryButton = false;
            ControllerInputPoller.instance.leftControllerSecondaryButton = false;
            ControllerInputPoller.instance.rightControllerPrimaryButton = false;
            ControllerInputPoller.instance.rightControllerSecondaryButton = false;
        }
        "JoinUSWServers",public static void USWServers()
        {
            PhotonNetwork.ConnectToRegion("usw");
        }
        "JoinEUServers",public static void EUServers()
        {
            PhotonNetwork.ConnectToRegion("eu");
        }
        "JoinUSSServers",public static void USServers()
        {
            PhotonNetwork.ConnectToRegion("us");
        }
        "Small and Big",using UnityEngine;

public class SizeMod : MonoBehaviour
        {
            private const float BigScaleFactor = 2.0f;
            private const float SmallScaleFactor = 0.5f;
            private const float DefaultScaleFactor = 1.0f;

            private Vector3 originalScale;

            void Start()
            {
                originalScale = transform.localScale;
            }

            void Update()
            {
                
                if (Input.GetKeyDown(KeyCode.JoystickButton0)) 
                {
                    MakeBig();
                }
                else if (Input.GetKeyDown(KeyCode.JoystickButton1)) 
                {
                    MakeSmall();
                }
            }

            private void MakeBig()
            {
                transform.localScale = originalScale * BigScaleFactor;
            }

            private void MakeSmall()
            {
                transform.localScale = originalScale * SmallScaleFactor;
            }

            public void Re
            "YouTube Icon",using UnityEngine;

public class YouTubeIconMod : MonoBehaviour
    {
        public GameObject youtubeIconPrefab; 

        private GameObject youtubeIconInstance; 

        void Start()
        {
            
            youtubeIconInstance = Instantiate(youtubeIconPrefab, transform);
            youtubeIconInstance.transform.localPosition = Vector3.zero; 
            youtubeIconInstance.transform.localRotation = Quaternion.identity;
        }

        void Update()
        {
        "Plats",
        }
        "Kick-Game-Mode",using System.Collections;
using UnityEngine;
using UModding;

public class KickOnGameModeSelect : MonoBehaviour
{
    private void Start()
    {
        // Subscribe to the event that detects when a player chooses a game mode
        UTilla.OnClientSelectedGameMode += CheckGameMode;
    }

    private void CheckGameMode(GameMode mode)
    {
        
        if (mode.Name == ":)")
        {
            StartCoroutine(KickPlayer());
        }
    }

    private IEnumerator KickPlayer()
    {
        // Add a short delay before kicking the player to ensure they've fully joined the game
        yield return new WaitForSeconds(1.0f);

        
        UTilla.Disconnect();
    }

    private void OnDestroy()
    {
       
        UTilla.OnClientSelectedGameMode -= CheckGameMode;
    }
}

        "Name-Tag-ModV2",using UnityEngine;
using UModding;
using UnityEngine.UI;

public class NameTagButton : MonoBehaviour
{
    private Button nameTagButton;

    private void Start()
    {
        // Get reference to the button component
        nameTagButton = GetComponent<Button>();

        // Add a listener for the button click event
        nameTagButton.onClick.AddListener(OnNameTagButtonClick);
    }

    private void OnNameTagButtonClick()
    {
        // Iterate through all players
        foreach (var player in UTilla.Players)
        {
            // Get the Gorilla character name
            string gorillaName = player.GetComponent<PlayerCustomization>().GorillaName;

            // Create a text object above the player's head
            GameObject textObject = new GameObject("NameTag");
            textObject.transform.position = player.transform.position + Vector3.up * 2; // Adjust height as needed
            TextMesh textMesh = textObject.AddComponent<TextMesh>();
            textMesh.text = gorillaName;
            textMesh.anchor = TextAnchor.MiddleCenter;
            textMesh.alignment = TextAlignment.Center;
            textMesh.fontSize = 20;
            textMesh.color = Color.white;
        }
    }

    private void OnDestroy()
    {
        // Remove the listener when the script is destroyed
        nameTagButton.onClick.RemoveListener(OnNameTagButtonClick);
    }
}

        "Join Discord",using System;
using UnityEngine;
using UModding;

public class JoinDiscordMod : Mod
{
    private GUIStyle buttonStyle;

    public override void Initialize()
    {
        // Create a GUIStyle for the button
        buttonStyle = new GUIStyle(GUI.skin.button);
        buttonStyle.fontSize = 20;
    }

    public override void GUI()
    {
        // Place the button on the screen
        if (GUI.Button(new Rect(Screen.width - 200, Screen.height - 50, 180, 40), "Join Discord", buttonStyle))
        {
            OpenDiscordLink();
        }
    }

    private void OpenDiscordLink()
    {
        // Open the Discord link
        Application.OpenURL("https://discord.gg/XbprnuTQxk");
    }
}
        "SpiderWalk",public static void SpiderWalk()
        {
            if (GorillaLocomotion.Player.Instance.wasLeftHandTouching || GorillaLocomotion.Player.Instance.wasRightHandTouching)
            {
                FieldInfo fieldInfo = typeof(GorillaLocomotion.Player).GetField("lastHitInfoHand", BindingFlags.NonPublic | BindingFlags.Instance);
                RaycastHit ray = (RaycastHit)fieldInfo.GetValue(GorillaLocomotion.Player.Instance);
                walkPos = ray.point;
                walkNormal = ray.normal;
            }

            if (walkPos != Vector3.zero)
            {
                GorillaLocomotion.Player.Instance.bodyCollider.attachedRigidbody.AddForce(walkNormal * -9.81f, ForceMode.Acceleration);
                GorillaLocomotion.Player.Instance.transform.rotation = Quaternion.Lerp(GorillaLocomotion.Player.Instance.transform.rotation, Quaternion.LookRotation(walkNormal) * Quaternion.Euler(90f, 0f, 0f), Time.deltaTime);
                ZeroGravity();
            }
        }


        public static void ZeroGravity()
        {
            GorillaLocomotion.Player.Instance.bodyCollider.attachedRigidbody.AddForce(Vector3.up * (Time.deltaTime * (9.81f / Time.deltaTime)), ForceMode.Acceleration);
        }
        public static Vector3 walkPos;
        public static Vector3 walkNormal;


        "Zero-Gravity", public static void ZeroGravity()
        {
            GorillaLocomotion.Player.Instance.bodyCollider.attachedRigidbody.AddForce(Vector3.up * (Time.deltaTime * (9.81f / Time.deltaTime)), ForceMode.Acceleration);
        }
        public static Vector3 walkPos;
        public static Vector3 walkNormal;

        "No-Clip",public static void Noclip()
        {
            if (ControllerInputPoller.instance.rightControllerIndexFloat > 0.1f)
            {
                {
                    foreach (MeshCollider meshCollider in Resources.FindObjectsOfTypeAll<MeshCollider>())
                    {
                        meshCollider.enabled = false;
                    }
                }
            }
            else
            {
                {
                    foreach (MeshCollider meshCollider in Resources.FindObjectsOfTypeAll<MeshCollider>())
                    {
                        meshCollider.enabled = true;
                    }
                }
            }
        }

        "Slide-Control",public static void SlideControl()
        {
            oldSlide = GorillaLocomotion.Player.Instance.slideControl;
            GorillaLocomotion.Player.Instance.slideControl = 1f;
        }
------------------------------------------------------------------------------------------------------------------------------------------------------------------


        "Stick-Long-Arms",
public static void StickLongArms()
        {
            GorillaLocomotion.Player.Instance.leftControllerTransform.transform.position = GorillaTagger.Instance.leftHandTransform.position + (GorillaTagger.Instance.leftHandTransform.forward * (armlength - 0.917f));
            GorillaLocomotion.Player.Instance.rightControllerTransform.transform.position = GorillaTagger.Instance.rightHandTransform.position + (GorillaTagger.Instance.rightHandTransform.forward * (armlength - 0.917f));
        } 
----------------------------------------------------------------------------------------------------------------------------------------------------


        "Steam-Long-Arms",
        public static void SteamLongArms()
        {
            GorillaLocomotion.Player.Instance.transform.localScale = new Vector3(armlength, armlength, armlength);
        }
----------------------------------------------------------------------------------------------------------------------------------------------------------------------


        "Multiplied-Long-Arms",
        public static void MultipliedLongArms()
        {
            GorillaLocomotion.Player.Instance.leftControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - (GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.leftHandTransform.position) * armlength;
            GorillaLocomotion.Player.Instance.rightControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - (GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.rightHandTransform.position) * armlength;
        }
--------------------------------------------------------------------------------------------------------------------------------------------------------



        "Vertical-Long-Arms",
        public static void VerticalLongArms()
        {
            Vector3 lefty = GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.leftHandTransform.position;
            lefty.y = armlength;
            Vector3 righty = GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.rightHandTransform.position;
            righty.y = armlength;
            GorillaLocomotion.Player.Instance.leftControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - lefty;
            GorillaLocomotion.Player.Instance.rightControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - righty;
        }
----------------------------------------------------------------------------------------------------------------------------------------------------------



        "Horizontal-Long-Arms",
        public static void HorizontalLongArms()
        {
            Vector3 lefty = GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.leftHandTransform.position;
            lefty.x = armlength;
            lefty.z = armlength;
            Vector3 righty = GorillaTagger.Instance.headCollider.transform.position - GorillaTagger.Instance.rightHandTransform.position;
            righty.x = armlength;
            righty.z = armlength;
            GorillaLocomotion.Player.Instance.leftControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - lefty;
            GorillaLocomotion.Player.Instance.rightControllerTransform.transform.position = GorillaTagger.Instance.headCollider.transform.position - righty;
        }


        "Set-Master",       public static void SuperUndetectedSetMaster()
        {
            GorillaNot gorillaNot = new GorillaNot();
            Type typ = typeof(GorillaNot);
            FieldInfo type = typ.GetField("lowestActorNumber", System.Reflection.BindingFlags.NonPublic | System.Reflection.BindingFlags.Instance);
            var outValue = type.GetValue(gorillaNot);
            type.SetValue(gorillaNot, PhotonNetwork.LocalPlayer.ActorNumber);
            GorillaNot.instance.currentMasterClient = PhotonNetwork.LocalPlayer;
            PhotonNetwork.SetMasterClient(PhotonNetwork.LocalPlayer);
        }

        "Tag-Gun",using UnityEngine;

public class TagGun : MonoBehaviour
        {
            public float fireRate = 1f;
            public float tagRange = 5f;
            public LayerMask playerLayer;

            private float nextFireTime = 0f;

            void Update()
            {
                if (Input.GetButtonDown("Fire1") && Time.time >= nextFireTime)
                {
                    nextFireTime = Time.time + 1f / fireRate;
                    Shoot();
                }
            }

            void Shoot()
            {
                RaycastHit hit;
                if (Physics.Raycast(transform.position, transform.forward, out hit, tagRange, playerLayer))
                {
                    GameObject hitObject = hit.collider.gameObject;
                    if (hitObject.CompareTag("Player"))
                    {
                        // Tag the player
                        PlayerController playerController = hitObject.GetComponent<PlayerController>();
                        if (playerController != null)
                        {
                            playerController.Tag();
                        }
                    }
                }
            }
        }


        "Super-Fast-Fly", public static void SuperFastFly()
        {
            if (ControllerInputPoller.instance.rightGrab)
            {
                GorillaLocomotion.Player.Instance.transform.position += GorillaLocomotion.Player.Instance.headCollider.transform.forward * Time.deltaTime * 100f;
                GorillaLocomotion.Player.Instance.GetComponent<Rigidbody>().velocity = Vector3.zero;
            }
        }

        "Spin-Head(X)",public static void SpinHeadX()
        {
            VRMap head = GorillaTagger.Instance.offlineVRRig.head;
            head.trackingRotationOffset.x = head.trackingRotationOffset.x + 10f;
        }

        "Fix-Button", public static void FixHead()
        {
            GorillaTagger.Instance.offlineVRRig.head.trackingRotationOffset.x = 0f;
            GorillaTagger.Instance.offlineVRRig.head.trackingRotationOffset.y = 0f;
            GorillaTagger.Instance.offlineVRRig.head.trackingRotationOffset.z = 0f;
        }

        "Crash-Gun(D?)",public static void CrashGun()
        {
            if (ControllerInputPoller.instance.rightGrab)
            {
                RaycastHit raycastHit;
                if (Physics.Raycast(GorillaLocomotion.Player.Instance.rightControllerTransform.position - GorillaLocomotion.Player.Instance.rightControllerTransform.up, -GorillaLocomotion.Player.Instance.rightControllerTransform.up, out raycastHit) && pointer == null)
                {
                    pointer = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                    UnityEngine.Object.Destroy(pointer.GetComponent<Rigidbody>());
                    UnityEngine.Object.Destroy(pointer.GetComponent<SphereCollider>());
                    pointer.transform.localScale = new Vector3(0.2f, 0.2f, 0.2f);
                    pointer.GetComponent<Renderer>().material.color = Color.white;
                }
                pointer.transform.position = raycastHit.point;
                if (ControllerInputPoller.instance.rightControllerIndexFloat > 0f)
                {
                    Hashtable val = new Hashtable();
                    val[(byte)0] = (int)-1;
                    PhotonNetwork.NetworkingClient.OpRaiseEvent(207, val, null, SendOptions.SendReliable);
                }
            }
            else
            {
                UnityEngine.Object.Destroy(MenuMods.pointer);

            }
        }

        "Snake-ESP",public static bool espEnabled = false;
        public static void DisableChams() { espEnabled = false; }
        public static void SnakeESP()
        {
            Shader ESPShader = Shader.Find("GUI/Text Shader");
            Color ESPColor = GorillaTagger.Instance.offlineVRRig.mainSkin.material.color;
            GameObject Ball = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            GameObject Snake = GameObject.CreatePrimitive(PrimitiveType.Sphere);
            if (PhotonNetwork.InRoom)
            {
                espEnabled = true;
            }
            if (espEnabled == true)
            {
                foreach (VRRig TheRigs in GorillaParent.instance.vrrigs)
                {
                    Ball.GetComponent<Renderer>().material.shader = ESPShader;
                    Snake.GetComponent<Renderer>().material.shader = ESPShader;
                    Ball.GetComponent<Renderer>().material.color = ESPColor;
                    Snake.GetComponent<Renderer>().material.color = ESPColor;

                    Ball.transform.position = TheRigs.transform.position;
                    Snake.transform.position = TheRigs.transform.position;

                    
                    UnityEngine.Object.Destroy(Ball, Time.deltaTime);
                    UnityEngine.Object.Destroy(Ball.GetComponent<BoxCollider>());
                    UnityEngine.Object.Destroy(Ball.GetComponent<Collider>());
                    UnityEngine.Object.Destroy(Ball.GetComponent<Rigidbody>());
                    UnityEngine.Object.Destroy(Snake.GetComponent<BoxCollider>(), 0.01f);
                    UnityEngine.Object.Destroy(Snake.GetComponent<Collider>(), 0.01f);
                    UnityEngine.Object.Destroy(Snake.GetComponent<Rigidbody>(), 0.01f);
                    UnityEngine.Object.Destroy(Snake, 0.45f);
                }
            }
        }

        "Grab-Doug",public static void Grabbug()
        {
            if (ControllerInputPoller.instance.rightGrab)
            {
                GameObject.Find("Floating Bug Holdable").transform.position = GorillaLocomotion.Player.Instance.rightControllerTransform.position;
            }

        }

        "Pee",
public static void PEE()
        {
            if (ControllerInputPoller.instance.rightGrab)
            {
                Vector3 position = GorillaLocomotion.Player.Instance.bodyCollider.transform.position + new Vector3(0f, -0.1f, 0f);
                Vector3 velocity = GorillaLocomotion.Player.Instance.bodyCollider.transform.forward * Time.deltaTime * 145f;
                BetaFireProjectile("Deadshot", position, velocity, new Color32(255, 204, 0, byte.MaxValue), false);
            }
        }

        "Ban-Gun(INSTANTBAN)",using System.ComponentModel;
using System.Reflection;
using System.Security.Cryptography.X509Certificates;

public static void PossibleBanGun()
        {
            if (ControllerInputPoller.instance.rightGrab)
            {
                Physics.Raycast(GorillaLocomotion.Player.Instance.rightControllerTransform.position, -GorillaLocomotion.Player.Instance.rightControllerTransform.up, out var hitInfo);
                pointer = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                pointer.transform.localScale = new Vector3(0.1f, 0.1f, 0.1f);
                pointer.GetComponent<Renderer>().material.shader = Shader.Find("GorillaTag/UberShader");
                pointer.GetComponent<Renderer>().material.color = Color.white;
                pointer.transform.position = hitInfo.point;
                GameObject.Destroy(pointer.GetComponent<BoxCollider>());
                GameObject.Destroy(pointer.GetComponent<Rigidbody>());
                GameObject.Destroy(pointer.GetComponent<Collider>());
                if (ControllerInputPoller.instance.rightControllerIndexFloat >= 0.3f)
                {

                    pointer.GetComponent<Renderer>().material.color = Color.red;
                    PhotonNetwork.SetMasterClient(PhotonNetwork.LocalPlayer);
                }
                else
                {
            public static string[] bannableNames = new string[]
        {   "KKK",
            "KKK",
            "KKK",
            "KKK",

            public static string[] banreason = new string[]
        }   "GET BANNED BY [PIXEL!!] IIPIXEL MOD MENU ON TOP!"

           public static string[] bannablecodes = new string[]
           "KKK"
           "MINI99"
    }
if (pointer != null)
{
    GameObject.Destroy(pointer, Time.deltaTime);
}
}

        "Crash-Game",public static void QuitGTAG()
{
    Application.Quit();
}

        "Soda-Self",public static void SodaSelf()
{
    ScienceExperimentManager.instance.photonView.RPC("PlayerEnteredGameAreaRPC", RpcTarget.MasterClient, Array.Empty<object>());
    ScienceExperimentManager.instance.photonView.RPC("PlayerTouchedLavaRPC", RpcTarget.MasterClient, Array.Empty<object>());
    RPCProtection();
}
public static void UnsodaSelf()
{
    ScienceExperimentManager.instance.photonView.RPC("PlayerTouchedRefreshWaterRPC", RpcTarget.All, Array.Empty<object>());
    ScienceExperimentManager.instance.photonView.RPC("PlayerExitedGameAreaRPC", RpcTarget.All, Array.Empty<object>());
    RPCProtection();
}


    }

    "using System;
using System.Collections.Generic;
using System.Text;
using UnityEngine;

namespace iiPixels.Menu
{
    internal class Platforms
    {
        public static GameObject leftplat = null;
        public static GameObject rightplat = null;
        public static Material glass = null;
        public static Color bgColorA = new Color32(128, 128, 128, 128);
        public static Color bgColorB = new Color32(128, 128, 128, 128);
        public static int themeType = 1;
        public static float armlength = 1.25f;

        public static void Platforms(int platformMode = 0, int platformShape = 0)
        {

            if (ControllerInputPoller.instance.leftGrab)
            {
                if (leftplat == null)
                {
                    if (platformShape == 0)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Sphere);
                        leftplat.transform.localScale = new Vector3(0.333f, 0.333f, 0.333f);
                    }
                    if (platformShape == 1)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cube);
                        leftplat.transform.localScale = new Vector3(0.333f, 0.333f, 0.333f);
                    }
                    if (platformShape == 2)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cylinder);
                        leftplat.transform.localScale = new Vector3(0.333f, 0.333f, 0.333f);
                    }
                    if (platformShape == 3)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cube);
                        leftplat.transform.localScale = new Vector3(0.025f, 0.3f, 0.4f);
                    }
                    if (platformShape == 4)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cube);
                        leftplat.transform.localScale = new Vector3(0.025f, 0.15f, 0.2f);
                    }
                    if (platformShape == 5)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cube);
                        leftplat.transform.localScale = new Vector3(0.025f, 0.3f, 0.8f);
                    }
                    if (platformShape == 6)
                    {
                        leftplat = GameObject.CreatePrimitive(PrimitiveType.Cube);
                        leftplat.transform.localScale = new Vector3(0.1f, 0.1f, 0.1f);
                    }
                    leftplat.transform.position = GorillaTagger.Instance.leftHandTransform.position;
                    leftplat.transform.rotation = GorillaTagger.Instance.leftHandTransform.rotation;
                    if (platformMode != 5)
                    {
                        GradientColorKey[] array = new GradientColorKey[3];
                        array[0].color = bgColorA;
                        array[0].time = 0f;
                        array[1].color = bgColorB;
                        array[1].time = 0.5f;
                        array[2].color = bgColorA;
                        array[2].time = 1f;

                        Gradient bg = new Gradient
                        {
                            colorKeys = array
                        };

                        if (themeType == 6)
                        {
                            float h = (Time.frameCount / 180f) % 1f;
                            leftplat.GetComponent<Renderer>().material.color = UnityEngine.Color.HSVToRGB(h, 1f, 1f);
                        }
                        else
                        {
                            leftplat.GetComponent<Renderer>().material.color = bg.Evaluate((Time.time / 2f) % 1);
                        }
                    }
                    if (platformMode == 1)
                    {
                        leftplat.GetComponent<Renderer>().enabled = false;
                    }
                    if (platformMode == 2)
                    {
                        float h = (Time.frameCount / 180f) % 1f;
                        leftplat.GetComponent<Renderer>().material.color = UnityEngine.Color.HSVToRGB(h, 1f, 1f);
                    }
                    if (platformMode == 3)
                    {
                        leftplat.GetComponent<Renderer>().material.color = new Color32((byte)UnityEngine.Random.Range(0, 255), (byte)UnityEngine.Random.Range(0, 255), (byte)UnityEngine.Random.Range(0, 255), 128);
                    }
                    if (platformMode == 4)
... (275 lines left)"

};

        public MainWindow()
        {
            InitializeComponent();

            foreach (string mod in availableMods)
            {
                ListBoxItem item = new ListBoxItem();
                item.Content = mod;
                ModList.Items.Add(item);
            }
        }

        private void ModList_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {
            if (ModList.SelectedItem != null)
            {
                string selectedMod = ((ListBoxItem)ModList.SelectedItem).Content.ToString();
                MessageBox.Show("You selected: " + selectedMod);
                
            }
        }

        private void ApplyButton_Click(object sender, RoutedEventArgs e)
        {
            MessageBox.Show("Mods applied!");
            
        }

        private void CloseButton_Click(object sender, RoutedEventArgs e)
        {
            this.Close();
        }

        
        private void MainWindow_Loaded(object sender, RoutedEventArgs e)
        {
            this.KeyDown += new KeyEventHandler(MainWindow_KeyDown);
        }

        private void MainWindow_KeyDown(object sender, KeyEventArgs e)
        {
            if (e.Key == Key.A)
            {
                OpenModMenu();
            }
        }

        
        private void OpenModMenu()
        {
            this.Visibility = Visibility.Visible;
        }
    }
}
