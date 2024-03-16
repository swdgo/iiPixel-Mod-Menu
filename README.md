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
