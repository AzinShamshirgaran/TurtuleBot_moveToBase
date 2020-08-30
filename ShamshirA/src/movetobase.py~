#!/usr/bin/env python
import rospy
import actionlib
from move_base_msgs.msg import MoveBaseAction, MoveBaseGoal
from geometry_msgs.msg import PoseStamped
from math import radians, degrees
from actionlib_msgs.msg import *
from geometry_msgs.msg import Point

#def movetoGoal():

 #   client = actionlib.SimpleActionClient('move_base',PoseStamped)
  #  client.wait_for_server()




class navigationWithMap():

    def __init__(self):

#seting the position of each corner in the Map 

        self.g1x = 3.57
        self.g1y = -0.68

        self.g2x = 3.5 
        self.g2y = -4.1

        self.g3x = -2.5
        self.g3y =-0.24

        self.g4x =- 4.68 
        self.g4y = -3.08

      
        self.goalReached = self.movetoGoal(self.g1x, self.g1y)

       

        self.goalReached = self.movetoGoal(self.g2x,self.g2y)

        

        self.goalReached = self.movetoGoal(self.g3x,self.g3y)

        

        self.goalReached = self.movetoGoal(self.g4x,self.g4y)

       

    def shutdown(self):
        rospy.loginfo("Exiting...")
        rospy.sleep()

    def movetoGoal(self,xGoal,yGoal):

#using actionlib to send the command to turtlebut
        client = actionlib.SimpleActionClient("move_base", MoveBaseAction)

        while(not client.wait_for_server(rospy.Duration.from_sec(5.0))):
            rospy.loginfo("Waiting for move_base action server to respond")

        goal = MoveBaseGoal()

        

        goal.target_pose.header.frame_id = "map"
        goal.target_pose.header.stamp = rospy.Time.now()

        

        goal.target_pose.pose.position = Point(xGoal,yGoal,0)
        goal.target_pose.pose.orientation.x = 0.0
        goal.target_pose.pose.orientation.y = 0.0
        goal.target_pose.pose.orientation.z = 0.0
        goal.target_pose.pose.orientation.w = 1.0
        
        rospy.loginfo("Sending goal...")
        client.send_goal(goal)

        client.wait_for_result(rospy.Duration(30))

#At first, I used PoseStamped, but it doesn't work for some reasons, so I changed the code to use Movebase Action 

   # goal = PoseStamped()
   # goal.header.frame_id = "map"
    #goal.header.stamp = rospy.Time.now()
    #goal.pose.position.z = 0
    #goal.pose.position.x = xGoal
    #goal.pose.position.y = yGoal
    #goal.pose.orientation.w = 1.0
    #client.send_goal(goal)
   # client.wait_for_result(rospy.Duration(60))
   # rospy.sleep(1)


if __name__ == '__main__':
    try:
        rospy.init_node('moveit', anonymous=False)
        result = navigationWithMap()
        if result:
            rospy.loginfo("Goal execution done!")
    except rospy.ROSInterruptException:
            rospy.loginfo("Navigation test finished.")
